<template>
  <!-- Explore More -->
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
window.$ = require("jquery");
window.JQuery = require("jquery");
export default {
  name: "App"
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
