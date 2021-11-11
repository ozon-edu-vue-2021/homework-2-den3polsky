<template>

      <div  class="directory"            
            @click.stop="select_handler"
            @keydown.enter.stop="select_handler"
            @keydown.space.prevent.stop="select_handler"
      > 
          <div class="directory-item" tabindex="1" :autofocus="1" @focus="emitSelect">

              <FolderIcon :isOpen="isOpen" />
              <div class="directory-name">{{tree.name}}</div>

          </div>

          <template v-if="isOpen">

                <div v-for="(item, index) in tree.contents" 
                      class="sub-tree"
                      :key="item.name + '-' + index"                   
                      @click.stop="select_handler(index, item.type)"
                      @keydown.enter.stop="select_handler(index, item.type)"
                      @keydown.space.prevent.stop="select_handler(index, item.type)"
                  >
                      <template v-if="item.type=='file'">

                          <File :name="item.name" :class="selectedClass(index)" @focus.native="emitSelect(index)" />

                      </template>

                      <template v-else-if="item.type=='link'">

                          <Link :name="item.name" :class="selectedClass(index)" :target="item.target"  @focus.native="emitSelect(index)" />

                      </template>                 

                      <template v-else-if="item.type=='directory'">

                          <Directory :tree="item" 
                                      :indexPath="[...indexPath, index]"
                                      :selectedPath="selectedPath"
                                      @select="emitRecursive($event, index)" 
                          />                          
                      </template>

                  </div>
            </template>
    </div>    

</template>


<script>

import FolderIcon from './icons/FolderIcon.vue'

import File from './File.vue'
import Link from './Link.vue'

export default {

  name: 'Directory',

  props: {

    tree: Object,       //директория, которая рендерится
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

    select_handler(index, item_type) {

      // емит индекс элемента, который был выбран, вверх родителю
      this.emitSelect(index)

      // изменяем признак открытости ветки
      if (item_type != 'link' && item_type != 'file') {

          this.isOpen = !this.isOpen    

      }   else {

          //Индекс выбранного элемента локально 
          this.selected =  (this.selected == index) ? -1 : index
      }
      
  },

    emitSelect(index) {
      
       Number.isInteger(index) ?                                   
            this.$emit('select', [index]) :
                  this.$emit('select', [])
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
          
          selected: -1,
          isOpen: false
      }

    },

}

</script>


<style scoped>

div {

   
    list-style-type: none;
    
    padding: 0;
}

li {

  position: relative;
  width: 100%;
 
  text-align: left;
  margin: 5px 0px 5px 5px;
 
}

.tree-wrapper {

  width: 100%;

}


.directory {

   
   width: 100%;
   cursor: pointer;
  display: block;

}

.directory-item {

  background-color: #ffff0021;
  display: flex;
  flex-direction: row;
  align-items: center;
}

.directory-name {
  width: 100%;
  text-align: left;
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


a {
  color: #42b983;
}

</style>
