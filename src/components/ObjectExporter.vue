<template>
<div></div>
</template>

<script>
//import * as BABYLON from 'babylonjs';
    export default {
        name: 'ObjectExporter', 
        mounted () {
            console.log("exporter component here")
            console.log("scene meshes: ", this.$parent.scene.meshes);
        }
    }
</script>

<style lang="css" scoped>

</style>