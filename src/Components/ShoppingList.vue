<script setup>
import { ref } from 'vue'

const lists = ref([])

fetch('http://localhost:3000/lists/', {
  method: 'GET',
  headers: { 'Content-type': 'application/json' }
})
  .then((res) => res.json())
  .then((item) => (lists.value = item))
  .then((item) => console.log(item))
</script>
<template>
  <div v-for="list in lists" :key="list.id">
    <h2>{{ list.title }}</h2>
    <ul>
      <li v-for="item in list.items" :key="item.id">
        {{ item.name }}
        {{ console.log(item) }}
      </li>
    </ul>
  </div>
</template>
