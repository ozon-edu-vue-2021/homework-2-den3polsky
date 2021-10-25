<template>
  <div id="app">

  <div class="nav"></div>

    <Directory :tree="tree" :level="0" />
  </div>
</template>

<script>

import Directory from './components/Directory.vue'
import tree from '../public/static/node_modules.json'


export default {
  name: 'App',
  components: {
    Directory
  },

  data() {
    return {
      tree
    }
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
  width: 50%;
 
}

.nav {
  
    top: 0px;
    height: 50px;
    background: white;
    border: 1px solid black;
    width: 100%;
    position: fixed; 
    z-index: 1;
}


</style>
