<script setup>
import HelloWorld from './components/HelloWorld.vue'
import { ref,onMounted,onBeforeMount,onBeforeUpdate,onUpdated } from 'vue'
const count=ref(0);
const source=ref(true);
onBeforeMount(()=>{
  console.log("1.beforeMount");
})

onMounted(()=>{
  console.log("2.Mounted");
})

onBeforeUpdate(()=>{
  console.log("3.before updated");
})

onUpdated(()=>{
  console.log("4.updated");
})

</script>

<template>
  <h1>parrent</h1>
  <button type="button" @click="count++">count is {{ count }}</button><br>
  <button @click="source=!source">toggle</button>
  <HelloWorld v-if="source"/>
</template>

<style scoped>

</style>
