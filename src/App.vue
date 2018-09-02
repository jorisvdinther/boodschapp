<template>
  <div id="app">
    
      <boodschapp></boodschapp>
  </div>
</template>

<script>
import boodschapp from './components/boodschapp.vue'

export default {
  name: 'app',
  components: {
    boodschapp
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
