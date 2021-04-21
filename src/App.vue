<template>
  <div id="app">
    <Map />
  </div>
</template>

<script>
import Map from './components/Map'

export default {
  name: 'App',
  components: {
    Map
  }
}
</script>

<style>
html, body, #app {
  height: 100%;
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
</style>
