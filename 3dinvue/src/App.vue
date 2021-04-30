<template>
  <div id="app">
    <Eddy />
  </div>
</template>

<script>
import Eddy from './components/Eddy.vue'

export default {
  name: 'App',
  components: {
    Eddy
  }
}
</script>

<style>
html,
body,
#app {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
