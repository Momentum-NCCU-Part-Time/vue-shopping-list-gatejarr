<script setup>
import { ref } from 'vue'
import AllLists from './Components/AllLists.vue'
import NewList from './Components/NewList.vue'
</script>

<template>
  <div id="header">
    <h1>Vue Shopping List</h1>
    <!-- <button @click.prevent="showNewList = true">New List</button> -->
    <NewList />
  </div>

  <div>
    <AllLists />
  </div>
</template>

<style scoped></style>
