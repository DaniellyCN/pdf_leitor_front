<template>
  <PdfChat/>
</template>

<script>
import PdfChat from './components/PdfChat.vue'

export default {
  name: 'App',
  components: {
    PdfChat
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
