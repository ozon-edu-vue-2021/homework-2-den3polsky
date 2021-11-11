<template>
    <div class="file" tabindex="1" >
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
}

</script>


<style scoped>


    .file {

        padding-left: 5px;
        background-color: #32cbff17;
    }

    .file-name {

        margin-left: 8px;
    }

     .selected {

        background-color: #1f70f7ad;
        outline: 2px solid #1818ffa8;
        border-radius: 5px;
       
    }

</style>
