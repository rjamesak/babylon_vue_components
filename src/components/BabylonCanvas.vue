<template>
    <div class="canvas">
        <canvas id="renderCanvas" touch-action="none"></canvas> <!-- touch-action="none" for best results from PEP -->
        <!-- <ModelLoader></ModelLoader> -->
        <!-- <model-loader v-if="isMounted" @model-params-received="loadModel"></model-loader> -->
        <model-loader v-if="isMounted"></model-loader>
        <Observables v-if="isMounted"></Observables>
        <Gizmos v-if="isMounted"></Gizmos>
        <ObjectExporter v-if="isMounted"></ObjectExporter>
    </div>
</template>

<script>
import * as BABYLON from 'babylonjs';
import 'babylonjs-loaders';
import ModelLoader from './ModelLoader.vue'
import Observables from './Observables.vue'
import Gizmos from './Gizmos.vue'
import ObjectExporter from './ObjectExporter.vue'
//import { BabylonFileLoaderConfiguration } from 'babylonjs';
    export default {
        name: 'BabylonCanvas', 
        components: {
            ModelLoader,
            Observables,
            Gizmos,
            ObjectExporter,
        },
        data() {
            return {
                isMounted: false,
            }
        },
        methods: {
            createScene() {
                this.scene = new BABYLON.Scene(this.engine);
                this.camera = new BABYLON.ArcRotateCamera("camera", -Math.PI / 2, Math.PI / 2.5, 3, new BABYLON.Vector3(0, 0, 0));
                this.camera.position = new BABYLON.Vector3(0, 10, -20);
                this.camera.wheelDeltaPercentage = 0.01;
                this.camera.attachControl(this.canvas, true);
                //this.scene.createDefaultLight();
                this.light = new BABYLON.HemisphericLight("light", new BABYLON.Vector3(0, 20, 0));
                this.makeFloor();

                return this.scene; 
            }, 
            makeFloor() {
                this.ground = BABYLON.MeshBuilder.CreateGround("ground", {width:10, height: 10 });
                this.ground.position = new BABYLON.Vector3(0, -0.5, 0);
                this.ground.isPickable = false;
            }, 
            go() {
                this.renderedScene = this.createScene();
                this.engine.runRenderLoop(() => {
                    this.renderedScene.render();
                })
            },
            addResizeListener() {
                window.addEventListener("resize", () => {
                    this.engine.resize();
                })
            },
            loadModel(params) {
                console.log("in canvas, model params emitted: ", params);
                BABYLON.SceneLoader.ImportMeshAsync(params.name, params.url, params.filename).then((result) => {
                    this.rootMesh = result.meshes[0];
                    this.rootMesh.position = new BABYLON.Vector3(0, 3, 0);
                    this.rootMesh.name = "parrot"
                    this.rootMesh.scaling.scaleInPlace(0.02)
                    //const birdAnim = scene.getAnimationGroupByName("parrot_A_")
                    //console.log("birdAnim: ", birdAnim)
                    }); // end model loading
            }
        },
        mounted () {
            this.canvas = document.querySelector("#renderCanvas");
            this.engine = new BABYLON.Engine(this.canvas, true);
            this.addResizeListener();
            this.go();
            this.isMounted = true;
        },
    }
</script>


<style lang="css" scoped>
#renderCanvas {
    width: 100%;
    height: 100%;
    touch-action: none;
    position: relative;
}
.canvas {
    width: 100%;
    height: 100%;
    position: relative;
}

</style>