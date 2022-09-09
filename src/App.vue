<template>
  <div id="app">
    <img alt="Net logo" src="./assets/netflix_logo_icon_124344.png">
    <MainBody />
  </div>
</template>

<script>

import MainBody from './components/MainBody.vue';

export default {
  name: 'App',
  components: {
    MainBody
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
