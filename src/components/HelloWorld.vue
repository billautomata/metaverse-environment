<script setup lang="ts">
import { ref } from "vue";

//@ts-ignore
import aframe from "aframe";
//@ts-ignore
import extras from "aframe-extras";

defineProps<{ msg: string }>();

const count = ref(0);

//@ts-ignore
const vikings = new Array(64)
  .fill(0)
  .map((o, i) => {
    return [Math.random(), Math.random()];
  })
  .map(o=> o.map(_o=>_o*40 - 20))

console.log(vikings)

console.log(aframe, extras);
</script>

<template>
  <a-scene fog stats>
    <a-entity camera look-controls wasd-controls="fly: true" position="0 3 0"/>
    <a-box
      position="-1 0.5 -8"
      rotation="0 45 0"
      color="#4CC3D9"
      shadow="receive: true; cast: true"
    ></a-box>
    <a-sphere
      position="-3 1.25 -5"
      radius="1.25"
      color="#EF2D5E"
      shadow="receive: true; cast: true"
    ></a-sphere>
    <!-- <a-entity light="type: directional; color: #EEE; intensity: 0.5; castShadow: true" position="-2 5 2"></a-entity> -->
    <a-entity
      light="type: point; color: #EEE; intensity: 0.5; castShadow: true"
      position="-2 5 2"
    ></a-entity>
    <a-entity
      v-for="(viking, idx) in vikings"
      v-bind:key="idx"
      v-bind:viking="viking"      
      :position="`${viking[0]} 0 ${viking[1]}`"
      :rotation="`0 ${Math.random()*360} 0`"
      scale="0.5 0.5 0.5"
      gltf-model="url(/metaverse-environment/untitled.glb)"
      animation-mixer
      shadow="receive: false"
    ></a-entity>
    <a-plane
      position="0 0 -4"
      rotation="-90 0 0"
      width="100"
      height="100"
      color="#7BC8A4"
      shadow="receive: true"
    ></a-plane>
    <a-sky color="#3366FF"></a-sky>
  </a-scene>
</template>

<style>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
</style>
