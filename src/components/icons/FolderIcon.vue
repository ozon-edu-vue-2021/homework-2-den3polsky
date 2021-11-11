<template>        
        <OpenFolderIcon v-if="isOpen"/>
        <CloseFolderIcon v-else/>            
</template>

<script>

import CloseFolderIcon from './CloseFolderIcon.vue'
import OpenFolderIcon from './OpenFolderIcon.vue'


export default {

    name: 'FolderIcon',

    props: {
        isOpen: Boolean,     
    },
    
    components: {
        CloseFolderIcon,   
        OpenFolderIcon,     
    }
}
</script>
