<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Essa é uma página criada com Vue.js e esse h1 foi passado por props"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
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
  margin-top: 180px;
}
</style>
