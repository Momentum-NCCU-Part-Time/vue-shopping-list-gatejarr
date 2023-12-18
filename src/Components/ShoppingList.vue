<script setup>
import { ref } from 'vue'

const lists = ref([])

fetch('http://localhost:3000/lists/', {
  method: 'GET',
  headers: { 'Content-type': 'application/jason' }
})
  .then((res) => res.json())
  .then((data) => (lists.value = data))
</script>
<template>
  <div v-for="list in lists" :key="list.id">
    <h2>{{ list.title }}</h2>
    <ul>
      <li v-for="item in lists" key="item.id">
        {{ list.items.item-name }}
      </li>
    </ul>
  </div>
</template>
