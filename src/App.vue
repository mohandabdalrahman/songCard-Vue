<template>
  <div id="app">
    <AppBar />
    <div class="container">
      <router-view />
      <Player />
    </div>
  </div>
</template>

<script>
import AppBar from "./components/AppBar";
import Player from "./components/Player";

export default {
  name: "App",
  components: {
    AppBar,
    Player
  },
  props: {}
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

a:hover {
  text-decoration: none;
}
</style>
