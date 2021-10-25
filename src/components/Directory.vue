<template>

  <div class="tree-wrapper">

        <li v-for="(item, index) in tree.contents" 
            :key="index"
            :tabindex="index + 1"
            :autofocus="index==0"
            @click.stop="close_open_handler(index)"
            @keydown.enter.stop="close_open_handler(index)"
            @focus="focus(item)"
        >
            <template v-if="item.type=='file'">

               <File :name="item.name"/>

            </template>

            <template v-else-if="item.type=='link'">

               <Link :name="item.name"/>

            </template>


            <div v-else class="tree-item directory-item"> 

                <template v-if="openMap[index]">
                  <OpenFolderIcon/>
                </template>

                <template v-else>
                    <CloseFolderIcon/>
                </template>

                <div>{{item.name}}</div>

            </div>


            <ul v-if="openMap[index]  && item.type == 'directory'" class="sub-tree" >

                <Directory :tree="item" :level="level + 1" />

            </ul>

        </li>

  </div>

</template>




<script>

import CloseFolderIcon from '/src/components/icons/CloseFolderIcon.vue'
import OpenFolderIcon from '/src/components/icons/OpenFolderIcon.vue'

import File from './File.vue'
import Link from './Link.vue'




export default {

  name: 'Directory',

  props: {
    tree: Object,
    level: Number
  },

  components: {
     OpenFolderIcon,
     CloseFolderIcon,
     File,
     Link
  },



  methods: {


    focus(item) {
      console.log(item)
    },


  close_open_handler(index) {



      if (!this.openMap[index]) this.openMap[index] = true
      else this.openMap[index] = !this.openMap[index]

      this.openMap = {...this.openMap}

    
      //this.$forceUpdate() 
   


  }


  },


data () {


    return {

         openMap: {}

        
    }

  },




}


</script>


<style scoped>
ul {
    display: flex;
  list-style-type: none;
    flex-direction: column;
   align-items: flex-start;
  padding: 0;
}
li {

  position: relative;
  display: block;
  margin: 5px 0px 5px 10px;
  text-align: left;
  cursor: pointer;
 
}

.tree-wrapper {
  width: 100%;
}


.tree-item {
  height: 35px;
  display: flex;
  flex-direction: row;
  align-items: center;
  box-shadow: 1px 1px 1px 1px #66666621;
}


.directory-item {
 background-color: #ffff0021;
}



.sub-tree {
  margin-left:30px;
  margin-top: 5px;
  margin-bottom: 5px;
}

.close-open {
  position: absolute;
  width: 100%;
  height: 100%;
  opacity: 0;
  cursor: pointer;
}

li:focus > .tree-item { 
  
    outline: dotted pink 2px !important;
}

li:focus {
  outline: none;
}


a {
  color: #42b983;
}

</style>
