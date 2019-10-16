<template>
  <div id="app">
    <Hangman/>
  </div>
</template>

<script>
import Hangman from './components/Hangman.vue';

export default {
  name: 'app',
  components: {
    Hangman,
  },
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
