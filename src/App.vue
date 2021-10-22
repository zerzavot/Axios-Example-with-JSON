<template>
  
  <div class="container">
    .row>.col-md-12
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Post from "./components/Post.vue"

export default {
  name: 'App',
  components: {
    Post,
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
  margin-top: 60px;
}
</style>
