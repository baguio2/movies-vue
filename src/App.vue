<template>
  <div id="app">
    <movies-layout/>
  </div>
</template>

<script>

import MoviesLayout from './layouts/movies-layout.vue';

export default {
  name: 'App',
  components: {
    MoviesLayout,
  },
  data() {
    return {
      info: null,
    };
  },
};
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
