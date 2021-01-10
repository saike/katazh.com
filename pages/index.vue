<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-flex class="katazh-title text-center">₭АTАѪ</v-flex>
      <v-row justify="center">
        <v-card width="450px" max-width="90vw" flat class="audio-player">
          <v-card-text class="px-6">
            <AudioPlayer :playlist="tracks"/>
          </v-card-text>
        </v-card>
      </v-row>
      <v-row class="mt-9" justify="center">
        <a href="https://t.me/katazh" target="_blank">
          <v-img :src="require('@/assets/img/join-us-on-telegram-button-icon.png')" width="200px" contain></v-img>
        </a>
      </v-row>
    </v-col>
  </v-row>
</template>

<script>
// import VuetifyAudio from 'vuetify-audio';
import AudioPlayer from '@/components/AudioPlayer';

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
    AudioPlayer
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
    opacity: 0.6;
    color: #fff; 
    line-height: 1 !important;

  }

  .audio-player {
    background-color: rgba(0,0,0,0.23) !important;
  }

</style>
