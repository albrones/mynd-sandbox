<template>
  <h1>MyNd Sandbox</h1>
  <h3>My developer sandbox for experiment and have fun.</h3>
  <div>
    <Home />
  </div>
</template>

<script>
import Home from "./components/Home.vue"

export default {
  name: "App",
  components: {
    Home,
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
