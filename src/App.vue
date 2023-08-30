<template>
  <DefaultHeader @connectEvent="connectEvent"/>
  <div v-if="connect" >
    <NuLinkTutorial />
  </div>
  <div v-else class="example">
    <NoConnect />
  </div>
</template>

<script setup >
import DefaultHeader from './components/DefaultHeader.vue'
import NoConnect from "@/components/NoConnect";
import NuLinkTutorial from "@/components/NuLinkTutorial"
import {ref} from "vue";
const connect = ref(false)
const connectEvent = (value) => {
  connect.value = value
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100vw;
}
body {
  margin: 0;
}
.example {
  text-align: center;
}
</style>
