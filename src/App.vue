<script setup>
import { ref } from 'vue'
import ShoppingList from './Components/ShoppingList.vue'
import NewList from './Components/NewList.vue'
</script>

<template>
  <div id="header">
    <h1>Vue Shopping List</h1>
    <!-- <button @click.prevent="showNewList = true">New List</button> -->
    <!-- your code here -->
  </div>
  <NewList />
  <div>
    <ShoppingList />
  </div>
</template>

<style scoped></style>
