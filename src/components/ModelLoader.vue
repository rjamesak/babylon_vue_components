<template>
    <div>
    </div>
</template>

<script>
import * as BABYLON from 'babylonjs';
    export default {
        name: 'ModelLoader', 
        methods: {
            getModel() {
                BABYLON.SceneLoader.ImportMeshAsync("", "http://localhost:8000/", "Parrot.glb").then((result) => {
                        
                    this.rootMesh = result.meshes[0];
                    this.rootMesh.position = new BABYLON.Vector3(0, 3, 0);
                    this.rootMesh.name = "parrot"
                    this.rootMesh.scaling.scaleInPlace(0.02)
                    //const birdAnim = scene.getAnimationGroupByName("parrot_A_")
                    //console.log("birdAnim: ", birdAnim)
                    this.$emit('model-created', this.rootMesh)
                        
                    }); // end model loading
                
            }, 
        },
        mounted () {
            //this.getModel();
            console.log('modelLoader here...')
            this.getModel();
            },
        }
</script>

<style lang="css" scoped>

</style>