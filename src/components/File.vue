<template>
    <div class="tree-item file-item" >
         <FileIcon/>
        <div class="file-name">{{name}}</div>
    </div>
</template>


<script>

    import FileIcon from '/src/components/icons/FileIcon.vue'


    export default {

    name: 'File',

    props: {
        name: String,    
    },

    components: {
        FileIcon
    },


    methods: {

    },

    data () {

        return {
            
        }


    },

}

</script>


<style scoped>


    .file-item  {

        padding-left: 5px;
        background-color: #32cbff17;
    }

    .file-name {

        margin-left: 8px;
    }

  li:focus > .file-item {

        background-color: #1f70f7ad;
        outline: 2px solid #1818ffa8;
        border-radius: 5px;
       
    }

</style>
