<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <CURD/>
</template>

<script>
import CURD from './components/CURD.vue'

export default {
  name: 'App',
  components: {
    CURD
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
