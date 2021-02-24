<template>
<div></div>
</template>

<script>
import * as BABYLON from 'babylonjs';
    export default {
        name: 'Gizmos', 
        mounted () {
            this.gizmoManager = new BABYLON.GizmoManager(this.$parent.scene);
            this.$parent.scene.onKeyboardObservable.add((kbInfo) => {
                if (kbInfo.type === BABYLON.KeyboardEventTypes.KEYDOWN) {
                        switch(kbInfo.event.key) {
                            case 'r':
                            console.log("KEY DOWN: ", kbInfo.event.key);
                            this.gizmoManager.rotationGizmoEnabled = !this.gizmoManager.rotationGizmoEnabled;
                            this.gizmoManager.positionGizmoEnabled = false;
                            this.gizmoManager.scaleGizmoEnabled = false;
                            this.gizmoManager.boundingBoxGizmoEnabled = false;
                            break;
                        // case 'c':
                        //     console.log("gizmos enabled: ", gizmosAreEnabled());
                        //     break;
                        case 'p':
                            this.gizmoManager.rotationGizmoEnabled = false;
                            this.gizmoManager.positionGizmoEnabled = !this.gizmoManager.positionGizmoEnabled;
                            this.gizmoManager.scaleGizmoEnabled = false;
                            this.gizmoManager.boundingBoxGizmoEnabled = false;
                            break;
                        case 'b':
                            this.gizmoManager.rotationGizmoEnabled = false;
                            this.gizmoManager.positionGizmoEnabled = false;
                            this.gizmoManager.scaleGizmoEnabled = false;
                            this.gizmoManager.boundingBoxGizmoEnabled = !this.gizmoManager.boundingBoxGizmoEnabled;
                            break;
                    }
                } // end if
            }) // end callback
            console.log("gizmo component here")
        }
    }
</script>

<style lang="css" scoped>

</style>