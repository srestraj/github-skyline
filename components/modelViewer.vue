<template>
  <div class="model-render">
    <img src="/capture.png" class="cursor-pointer screenshot" title="Take a snapshot" alt="screenshot" @click="snapshot">
    <model-stl
    ref="model"
    :backgroundAlpha="bgAlpha"
    :rotation="rotation"
    :backgroundColor="bgColor"
    :controlsOptions="{
        enablePan,
        enableZoom,
        enableRotate
    }"
    :src="'/models/' + year + '.stl'"
    :glOptions="{ preserveDrawingBuffer: true }"
     @on-load="rotateModel"
    />
    <img v-if="base64" class="snapshot h-32 md:h-40 w-32 md:w-40" :src="base64" />
  </div>
</template>

<script>
export default {
    props: {
        year: {
            type: String,
            default: '2019'
        },
        enablePan: {
            type: Boolean,
            default: true
        },
        enableZoom: {
            type: Boolean,
            default: true
        },
        enableRotate: {
            type: Boolean,
            default: true
        },
        bgColor: {
            type: String,
            default: '#13ce66'
        },
        bgAlpha: {
            type: Number,
            default: 0.5
        }
    },
    data () {
        return {
            intersected: null,
            rotation: {
                x: -Math.PI / 2,
                y: 0,
                z: Math.PI / 4
            },
            base64: null
        }
    },
    methods: {
        snapshot () {
            this.base64 = this.$refs.model.renderer.domElement.toDataURL('image/png', 1)
        },
        rotateModel () {
            this.rotation.z += 0.001
            requestAnimationFrame(this.rotateModel)
        }
    }
}
</script>

<style></style>
