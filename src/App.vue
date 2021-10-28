<template>
  <div id="app">

      <div class="nav">{{ makePathFromIndexes}}</div>

      <div class="directory-wrapper">

        <Directory :tree="tree" 
                  :selectedPath="path" 
                  :indexPath="[]" 
                  @select="showPath($event)" 
        />

      </div>

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

  methods: {
    
    showPath(path) {

      this.path = path

    },

  },

  computed: {

    //у нас есть путь до выранного элемента в индексном массиве path
    //Из него строим текстовый вариант
    
    makePathFromIndexes() {
     
        const stringPath = [tree.name]
        let node = tree
        this.path.forEach(index => {
            stringPath.push(node.contents[index].name)
            node = node.contents[index]
        })
    
        return stringPath.join('/')
    }

  },


  data() {

    return {

      tree,
      path: []

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
  width: 100%;
}

.directory-wrapper {
  max-width: 45%;
}

.nav {
  
    top: 0px;
    height: 40px;
    background: #202020;
    border: 1px solid black;
    width: 100%;
    position: fixed;
    z-index: 1;
    display: flex;
    align-items: center;
    color: white;
    font-size: 18px;
    padding-left: 10px;
}

.directory, .file, .link {
  
  min-height: 35px;
  display: flex;
  flex-direction: row;
  align-items: center;
  box-shadow: 1px 1px 1px 1px #66666621;

}

.directory-item:focus, .file:focus, .link:focus { 
  
    outline: dotted pink 3px !important;
}


</style>
