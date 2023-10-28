<template>
  <div id="app">
    <CustomSwiper />
  </div>
</template>

<script>
import CustomSwiper from './components/CustomSwiper.vue'

export default {
  name: 'App',
  components: {
    CustomSwiper
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
