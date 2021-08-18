<template>
  <main>
    <Container v-if="game" :climb="climb" @finish="finish"/>
    <Home v-else @playGame="playGame"/>
  </main>
</template>

<script>
import Container from './components/Container.vue'
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    Container,
    Home,
  },
  data(){
    return {
      game: false,
      climb: false,
    }
  },
  methods:{
    playGame(params){
      if(params){
        this.climb = true;
      }
      this.game = true;
    },
    finish(){
      this.game = false;
      this.climb = false;
    }
  }
}
</script>

<style lang="scss">
@import '@/styles/general.scss';
@import '@/styles/utilities.scss';
</style>
