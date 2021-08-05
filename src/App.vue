<template>
  <main>
    <Container/>
  </main>
</template>

<script>
import Container from './components/Container.vue'

export default {
  name: 'App',
  components: {
    Container,
  }
}
</script>

<style lang="scss">
@import '@/styles/general.scss';
@import '@/styles/utilities.scss';
</style>
