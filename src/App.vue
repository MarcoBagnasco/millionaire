<template>
  <main>
    <Container v-if="game" @finish="finish"/>
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
    }
  },
  methods:{
    playGame(){
      this.game = true;
    },
    finish(){
      this.game = false;
    }
  }
}
</script>

<style lang="scss">
@import '@/styles/general.scss';
@import '@/styles/utilities.scss';
</style>
