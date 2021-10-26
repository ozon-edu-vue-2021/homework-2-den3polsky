<template>
    <div class="link">
         <LinkIcon/>
        <div class="link-name">{{name}}</div>
        <div class="link-target">{{target}}</div>
        
    </div>
</template>


<script>

    import LinkIcon from '/src/components/icons/LinkIcon.vue'

    export default {

        name: 'LinkItem',

        props: {
            name: String,    
            target: String,    
        },

        components: {
            LinkIcon
        },
}
</script>


<style scoped>

    .link  {

        padding-left: 5px;
        background-color: #38ff0017;
    }

    .link-name {

        margin-left: 8px;
    }

    .selected {

        background-color: #67ff3c8f;
        outline: 2px solid #1c810017;
        border-radius: 5px;
       
    }

    .link-target {
        
        justify-self: end;
        margin-left: auto;
        padding-right: 10px;
    }


</style>
