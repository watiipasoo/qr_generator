<template>
  <HeaderBody/>
  <HelloWorld/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import HeaderBody from './components/Header.vue'

export default {
  name: 'App',
  components: {
    HeaderBody,
    HelloWorld,
  }
}
</script>

<style>
* {
    color: #00FFFF;
}

body{
  background-color: #2c3e50;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
