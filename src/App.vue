<template>
  <div id="app">
    <color-to-binary></color-to-binary>
  </div>
</template>

<script>
import ColorToBinary from './components/color-binary'

export default {
  name: 'app',
  components: {
    'color-to-binary': ColorToBinary
  }
}
</script>

<style>
body {
  background-color: #eeeeee;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
