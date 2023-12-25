<script setup>
import { ref } from 'vue'
import AddItem from './AddItem.vue'
import ListItems from './ListItems.vue'

const lists = ref([])
const purchased = ref(false)
const newItem = ref('')

fetch('http://localhost:3000/lists/', {
  method: 'GET',
  headers: { 'Content-type': 'application/json' }
})
  .then((res) => res.json())
  .then((data) => (lists.value = data))

</script>

<template>
  <div v-for="list in lists" :key="list.id">
    <h2>{{ list.title }}</h2>
    <AddItem :list="list" />
    <ListItems :list="list" />
  </div>
</template>
