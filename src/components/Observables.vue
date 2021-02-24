<template>
<div></div>
    
</template>

<script>
    export default {
        name: 'Observables', 
        data() {
            return {
            }
        },
        methods: {
        },
        mounted () {
            this.$parent.scene.onPointerDown = (evt, pickResult) => {
                console.log("pointer down, picked: ", pickResult);
                if(pickResult.pickedMesh) {
                    console.log("abs pos: ", pickResult.pickedMesh.absolutePosition)
                    console.log("pos: ", pickResult.pickedMesh.position)
                    console.log("quat: ", pickResult.pickedMesh.quaternion)
                    console.log("abs quat: ", pickResult.pickedMesh.absoluteRotationQuaternion)
                    console.log("abs scaling: ", pickResult.pickedMesh.absoluteScaling)
                }
            }
            console.log('Observable component here...')
            },
        }
</script>

<style lang="css" scoped>

</style>