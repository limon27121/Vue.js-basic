<script setup>
import { onMounted, onBeforeMount, onUnmounted,onBeforeUnmount } from 'vue';

onBeforeUnmount(()=>{
  console.log("5.before unmount");
})

onUnmounted(()=>{
  console.log("6.unmounted")
})

</script>

<template>
  <h1>Child</h1>

</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
