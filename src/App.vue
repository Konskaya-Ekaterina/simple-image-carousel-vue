<template>
  <image-carousel/>
</template>

<script>
import ImageCarousel from "./components/ImageCarousel";

export default {
  name: 'App',
  components: {
    ImageCarousel
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
  margin-top: 30px;
}
</style>