<template>
  <div id="app">
    <TheWheel msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import TheWheel from './components/TheWheel.vue'

export default {
  name: 'app',
  components: {
    TheWheel
  }
}
</script>

<style>
@import url('https://cdnjs.cloudflare.com/ajax/libs/modern-normalize/0.5.0/modern-normalize.css');
@import url('https://fonts.googleapis.com/css?family=Oswald:700');

html {
  background-color: #2ac6b6;
  background-image: url(https://cdn.dunk.town/images/DunktownTexture_v3.png);
  background-position: 50% 0;
  background-size: 1100px auto;
}

#app {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  width: 100%;
  overflow: hidden;
}
</style>
