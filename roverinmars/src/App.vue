<template>
  <div id="app">
      <Navbar></Navbar>
      <div class="mt-4">
    <router-view/>
      </div>
  </div>
</template>

<style>
html {
  background-color: rgb(211, 109, 81);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: rgb(211, 109, 81);
}

.tdn {
  text-decoration: none;
}
</style>

<script>
import Navbar from '@/components/Navbar.vue'

export default {
  name: "App",
  components: {
    Navbar
  }
}
</script>

