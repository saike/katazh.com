<template>
  
  <v-flex class="flex-column justify-center text-center">

    <v-flex class="mb-2">
      <span class="body-2 mx-4">{{ playlist[current] && playlist[current].title || 'Playlist is empty' }}</span>
    </v-flex>

    <v-flex class="mb-2">
      <div class="d-inline-block audio-player-volume-tool">
        <v-row dense align="center">
          <v-col cols="auto">
            <v-btn icon outlined small @click="mute">
              <v-icon small v-if="!muted && volume > 0">mdi-volume-high</v-icon>
              <v-icon small v-else color="error">mdi-volume-mute</v-icon>
            </v-btn>
          </v-col>
          <v-col>
            <v-slider
              v-model="volume"
              @change="changeVolume"
              max="1"
              min="0"
              step="0.01"
              color="white"
              hide-details
            ></v-slider>
          </v-col>
        </v-row>
      </div>
    </v-flex>
    

    <v-flex class="flex-row flex-nowrap justify-center mb-2">
      <v-btn class="ma-1" icon outlined v-if="playlist.length > 1" @click="prev">
        <v-icon>mdi-skip-backward</v-icon>
      </v-btn>
      <v-btn class="ma-1" icon outlined v-if="!playing" @click="play(current)">
        <v-icon>mdi-play</v-icon>
      </v-btn>       
      <v-btn class="ma-1" icon outlined v-if="playing" @click="pause">
        <v-icon>mdi-pause</v-icon>
      </v-btn>      
      <v-btn class="ma-1" icon outlined @click="stop">
        <v-icon>mdi-stop</v-icon>
      </v-btn>
      <v-btn class="ma-1" icon outlined v-if="playlist.length > 1" @click="next">
        <v-icon>mdi-skip-forward</v-icon>
      </v-btn>   
      <v-btn class="ma-1" icon outlined @click="download" :href="playlist[current].url" download>
        <v-icon>mdi-download</v-icon>
      </v-btn>
    </v-flex>

    <v-flex>
      <v-slider
        v-model="time"
        @change="changeTime"
        :max="audio.duration"
        min="0"
        step="0.01"
        color="primary"
        hide-details
      ></v-slider>   
    </v-flex>

    

  </v-flex>

</template>

<script>
export default {
  props: {
    playlist: {
      type: Array,
      default: () => ([])
    },
    startFrom: {
      type: Number,
      default: 0
    }
  },
  data(){
    return {
      playing: false,
      volume: 1,
      audio: false,
      current: 0,
      muted: false,
      time: 0,
      paused: false,
      progressChecker: false
    }
  },
  watch: {
    startFrom: {
      handler(startFrom){

        this.stop();
        this.current = startFrom;

      }
    }
  },
  methods: {
    play(index){

      if(this.paused) {
        this.playing = true;
        this.paused = false;
        this.audio.play();
        return;
      }

      let track = this.playlist[index];

      if(!track) return;
        
      if(track.url) {

        this.audio = new Audio(track.url);
        if(!this.muted) this.audio.volume = this.volume;
        this.audio.play();
        
        this.playing = true;

        this.audio.addEventListener('ended', () => {
          this.next();
        });

        // this.audio.addEventListener('progress', () => {
        //   this.time = this.audio.currentTime;
        // });
      }

      

    },
    pause(){

      if(this.audio) {
        this.paused = true;
        this.audio.pause();
        this.playing = false;
      }

    },
    stop(){

      if(this.audio) {
        this.audio.pause();
        this.audio.currentTime = 0;
        this.playing = false;
        this.paused = false;
        this.time = 0;
      }

    },
    next(){

      if(this.current < this.playlist.length - 1){

        this.current++;

        if(!this.playing) return;

        this.stop();

        this.play(this.current);

      } 

    }, 
    prev(){

      if(this.current > 0){

        this.current--;

        if(!this.playing) return;

        this.stop();

        this.play(this.current);

      } 

    },
    changeVolume(){

      if(!this.audio) return;
      this.audio.volume = this.volume;

    },
    mute(){

      this.muted = !this.muted;

      if(!this.audio) return;

      if(this.muted) {

        this.audio.volume = 0;

      }
      else {

        this.audio.volume = this.volume;

      }
    },
    changeTime(){

      if(!this.audio) return;

      this.audio.currentTime = this.time;

    },
    checkTime(){

      this.progressChecker = setInterval(() => {

        if(!this.audio || !this.playing) return;

        this.time = this.audio.currentTime;

      }, 100);

    }
  },
  mounted() {
    this.checkTime();
  },
  beforeDestroy(){
    this.progressChecker && clearInterval(this.progressChecker);
  }
}
</script>

<style lang="scss" scoped>

  .audio-player-volume-tool {

   width: 150px;

  }

</style>