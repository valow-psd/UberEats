<template>
  <div id="app">
    <Home/>
  </div>
</template>

<script>

import Home from './page/Home.vue';

export default {
  name: 'App',
  components: {
    Home,
  },
}
</script>

<style>
/*@import url('.styles/reset.css');*/
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap');

#app {
  font-family: Roboto;
  padding: 0px 20px;
}
</style>
