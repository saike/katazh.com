<template>
  <v-app dark class="app">
    
    <v-main>
      <v-container fluid fill-height>
        <nuxt />
      </v-container>
    </v-main>
    
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      
    }
  }
}
</script>

<style lang="scss" scoped>

  .app {
    background-image: url('/bg/background.jpg');
    background-size: cover;
    background-position: bottom center;
  }

</style>
