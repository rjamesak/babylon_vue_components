<template>
  <div id="app">
    <BabylonCanvas></BabylonCanvas>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import BabylonCanvas from './components/BabylonCanvas.vue'

export default {
  name: 'App',
  components: {
    BabylonCanvas
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  overflow: hidden;
}
</style>
