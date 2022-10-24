<template>

  <Viewer />
</template>

<script>
import Viewer from './components/Viewer.vue'

export default {
  name: 'App',
  components: {
    Viewer
  }
}
</script>

<style>
   * {
        margin: 0;
        padding: 0;
    }
    
    *,
    *::after,
    *::before {
        box-sizing: inherit;
    }
html,body{
  height: 100%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2e2e2e;

  position: relative;
  overflow:hidden;
  height:100%;

  
}
</style>
