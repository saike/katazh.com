<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-flex class="katazh-title text-center">₭АTАѪ</v-flex>
      <v-flex class="text-center">
        <div class="text-center white--text">
          <v-btn icon outlined @click="autoplay = true; current = current-1 < 0 ? tracks.length-1 : current-1;">
            <v-icon>mdi-skip-backward</v-icon>
          </v-btn>
          <span class="body-2 mx-4">{{ tracks[current].title }}</span>
          <v-btn icon outlined @click="autoplay = true; current = current+1 > tracks.length-1 ? 0 : current+1;">
            <v-icon>mdi-skip-forward</v-icon>
          </v-btn>
        </div>
        <VuetifyAudio :file="tracks[current].url" class="audio-player" :ended="() => { autoplay = true; current = current+1 > tracks.length-1 ? 0 : current+1; }" downloadable flat :auto-play="autoplay"/>  
      </v-flex>
    </v-col>
  </v-row>
</template>

<script>
import VuetifyAudio from 'vuetify-audio';

const tracks = [
  {
    title: 'Насрать',
    url: '/ddx/Katazh_Nasrat.wav'
  },
  {
    title: 'Катать',
    url: '/ddx/Katazh_Katat.wav'
  },
  {
    title: 'Нихуя',
    url: '/ddx/Katazh_Nihuya.wav'
  },
  {
    title: 'Не важно',
    url: '/ddx/Katazh_NeVazhno.wav'
  },
  {
    title: 'Не спешу',
    url: '/ddx/Katazh_NeSpeshu.wav'
  },
  {
    title: 'Такой же, как и ты',
    url: '/ddx/Katazh_Ruki.wav'
  },

];

export default {
  components: {
    VuetifyAudio
  },
  data(){

    return {
      current: 0,
      tracks,
      autoplay: false
    }

  }
}
</script>

<style lang="scss" scoped>

  .katazh-title {

    font-family: sans-serif;
    font-size: 25vw;
    opacity: 0.3;
    color: #fff; 
    line-height: 1 !important;

  }

  .audio-player {
    background-color: transparent !important;
  }

</style>
