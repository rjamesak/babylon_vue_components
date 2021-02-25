<template>
    <div>
    </div>
</template>

<script>
import * as BABYLON from 'babylonjs';
    export default {
        name: 'ModelLoader', 
        data() {
            return {
                sceneObjects:
                    [
                        {
                            name: "",
                            url: "http://localhost:8000/",
                            filename: "Parrot.glb",
                            position: {x: 0, y: 3, z: 0},
                            scaling: 0.02,
                        },
                        {
                            name: "",
                            url: "http://localhost:8000/",
                            filename: "Logo.gltf.glb",
                            position: {x: -2, y: 2, z: -1},
                            scaling: 0.1,
                        },
                        // {
                        //     name: "",
                        //     url: "http://localhost:8000/",
                        //     filename: "Logo.babylon",
                        //     position: {x: 2, y: 3, z: -1},
                        //     scaling: 0.1,
                        // }
                    ]
            }
        },
        methods: {
            getModel() {
                this.sceneObjects.forEach(mesh => {
                    BABYLON.SceneLoader.ImportMeshAsync(mesh.name, mesh.url, mesh.filename)
                    .then((result) => {
                        this.rootMesh = result.meshes[0];
                        this.rootMesh.position = new BABYLON.Vector3(mesh.position.x, mesh.position.y, mesh.position.z);
                        this.rootMesh.name = mesh.name
                        this.rootMesh.scaling.scaleInPlace(mesh.scaling)
                        //const birdAnim = scene.getAnimationGroupByName("parrot_A_")
                        //console.log("birdAnim: ", birdAnim)
                        this.$emit('model-created', this.rootMesh)
                            
                        }); // end model loading

                })
               
                
            }, 
        },
        mounted () {
            // fetch parameters
            console.log('modelLoader here...')
            this.getModel();
            console.log("scene: ", this.scene);
            },
        }
</script>

<style lang="css" scoped>

</style>