<script setup>
import { ref } from 'vue'
import AllLists from './Components/AllLists.vue'
</script>

<template>
  <div id="header">
    <h1>GateJarr's Vue Shopping List</h1>
  </div>

  <div class="mainPage">
    <AllLists />
  </div>
</template>

<style scoped>
#header {
  font-family: 'Courier New', Courier, monospace;
}
</style>
