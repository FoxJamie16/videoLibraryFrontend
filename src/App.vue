<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to VideoLibrary - Upload and retrieve videos below!"/>
  <videoUploader></videoUploader>
  <videoGetter></videoGetter>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import videoUploader from './components/videoUploader.vue'
import videoGetter from './components/videoGetter.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    videoUploader,
    videoGetter,
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
