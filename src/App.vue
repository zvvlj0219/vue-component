<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <hr>
    <VslotComponent >
      <template v-slot:hello><p>HelloWorld</p></template>
    </VslotComponent>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import VslotComponent from './components/VslotComponent.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    VslotComponent
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
