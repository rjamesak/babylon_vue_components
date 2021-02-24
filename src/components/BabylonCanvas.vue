<template>
    <div>
        <canvas id="renderCanvas" touch-action="none"></canvas> <!-- touch-action="none" for best results from PEP -->
        <!-- <ModelLoader></ModelLoader> -->
        <model-loader></model-loader>
    </div>
</template>

<script>
import * as BABYLON from 'babylonjs';
import ModelLoader from './ModelLoader.vue'
//import { BabylonFileLoaderConfiguration } from 'babylonjs';
    export default {
        name: 'BabylonCanvas', 
        components: {
            ModelLoader,
        },
        methods: {
            createScene() {
                this.scene = new BABYLON.Scene(this.engine);
                this.camera = new BABYLON.ArcRotateCamera("camera", -Math.PI / 2, Math.PI / 2.5, 3, new BABYLON.Vector3(0, 0, 0));
                this.camera.position = new BABYLON.Vector3(0, 10, -20);
                this.camera.attachControl(this.canvas, true);
                //this.scene.createDefaultLight();
                this.light = new BABYLON.HemisphericLight("light", new BABYLON.Vector3(0, 20, 0));
                this.makeFloor();

                return this.scene; 
            }, 
            makeFloor() {
                this.ground = BABYLON.MeshBuilder.CreateGround("ground", {width:10, height: 10 });
                this.ground.position = new BABYLON.Vector3(0, -0.5, 0);
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
            }
        },
        mounted () {
            this.canvas = document.querySelector("#renderCanvas");
            this.engine = new BABYLON.Engine(this.canvas, true);
            this.addResizeListener();
            this.go();
        },
    }
</script>


<style lang="css" scoped>
#renderCanvas {
    width: 100%;
    height: 100%;
    touch-action: none;
}

</style>