<template>
  <img alt="Vue logo" src="./assets/phoenix.png">
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <AttributePage></AttributePage>
</template>

<script>
import AttributePage from './components/AttributePage.vue';
// import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'App',
  components: {
    AttributePage
    // , HelloWorld
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
