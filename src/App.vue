<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <ButtonsObject num=1 />
    <ButtonsObject num=2 />
    <ButtonsObject num=3 />
    <ButtonsObject num=4 />
    <ButtonsObject num=5 />
    <ButtonsObject num=6 />
    <ButtonsObject num=7 />
    <ButtonsObject num=8 />

    <half-circle-spinner
  :animation-duration="1000"
  :size="300"
  color="#000000"
/>

  </div>
</template>

<script>
import { HalfCircleSpinner } from 'epic-spinners'

import HelloWorld from './components/HelloWorld.vue'
import ButtonsObject from './components/ButtonsObject.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,
    ButtonsObject,
    HalfCircleSpinner
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
