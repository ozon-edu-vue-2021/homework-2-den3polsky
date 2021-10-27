<template>

  <div class="tree-wrapper">

        <li v-for="(item, index) in tree.contents" 
            :key="item.name + '-' + index"
            tabindex="1"
            :autofocus="index==0"
            @click.stop="select_handler(index)"
            @keydown.enter.stop="select_handler(index)"
            @keydown.space.prevent.stop="select_handler(index)"
        >
            <template v-if="item.type=='file'">

               <File :name="item.name" :class="selectedClass(index)"  />

            </template>

            <template v-else-if="item.type=='link'">

               <Link :name="item.name" :target="item.target" :class="selectedClass(index)"  />

            </template>


            <div v-else class="directory"> 

                <FolderIcon :isOpen="openedMap[index]" />

                <div>{{item.name}}</div>
                  
            </div>

            <ul v-if="openedMap[index]  && item.type == 'directory'" class="sub-tree" >

                <Directory :tree="item" 
                           :indexPath="[...indexPath, index]"
                           :selectedPath="selectedPath"
                           @select="emitRecursive($event, index)" 
                />

            </ul>

        </li>

  </div>

</template>


<script>

import Vue from 'vue'

import FolderIcon from '/src/components/icons/FolderIcon.vue'

import File from './File.vue'
import Link from './Link.vue'

export default {

  name: 'Directory',

  props: {

    tree: Object,       //поддерево, которое рендерится
    indexPath: Array,   //путь из индексов до этого поддерева, например [2, 4, 5, 0]
    selectedPath: Array //путь до выбранного элемента

  },
  

  components: {
     FolderIcon,   
     File,
     Link
  },

  methods: {

    emitRecursive(event, index)  {
        //передаем путь на выбранном элементе вверх к предкам рекурсивно
        this.$emit('select', [index, ...event]);          
    },


    select_handler(index) {

       //Индекс выбранного элемента локально
      this.selected =  (this.selected == index) ? -1 : index


      // передаем индекс элемента, который был выбран 
      this.$emit('select', [index])


    
      // изменяем признак открытости ветки
      const nodeState = this.openedMap[index]
      Vue.set(this.openedMap, index, !nodeState)

  },


    selectedClass(index) {

      


        //элемент считаем выделенным
        if (index == this.selected && // если выделен локально
          //и путь до элемента совпадает с текущим выделенным путем
          JSON.stringify(this.selectedPath.slice(0, -1)) ==  JSON.stringify(this.indexPath)
        )

        return {selected: true}

    }

  },

  data () {

      return {

          openedMap: {},
          selected: -1,

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
  margin: 5px 0px 5px 5px;
  text-align: left;
  cursor: pointer;
 
}

.tree-wrapper {

  width: 100%;

}


.directory {

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

li:focus > div { 
  
    outline: dotted pink 3px !important;
}

li:focus {
  outline: none;
}

a {
  color: #42b983;
}

</style>
