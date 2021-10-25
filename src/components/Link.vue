<template>
    <div class="tree-item link-item">
         <LinkIcon/>
        <div class="link-name">{{name}}</div>
    </div>
</template>


<script>

    import LinkIcon from '/src/components/icons/LinkIcon.vue'


    export default {

    name: 'LinkItem',

    props: {
        name: String,    
    },

    components: {
        LinkIcon
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


    .link-item  {

        padding-left: 5px;
        background-color: #38ff0017;
    }

    .link-name {

        margin-left: 8px;
    }

    li:focus > .link-item {

        background-color: #67ff3c8f;
        outline: 2px solid #1c810017;
        border-radius: 5px;
       
    }

</style>
