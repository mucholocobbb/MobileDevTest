<template>
  <div id="app">
    <Picbutton msg="Welcome & Enjoy"/>
  </div>
</template>

<script>
import Picbutton from './components/Picbutton.vue'

export default {
  name: 'App',
  components: {
    Picbutton
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 24px;
}
</style>
