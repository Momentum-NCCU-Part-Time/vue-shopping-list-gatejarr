<script setup>
import { ref } from 'vue'
import ShoppingList from './Components/ShoppingList.vue'
</script>

<template>
  <div id="header">
    <h1>Vue Shopping List</h1>
    <button>New List</button>
    <!-- your code here -->
  </div>
  <div>
    <ShoppingList />
  </div>
</template>

<style scoped></style>
