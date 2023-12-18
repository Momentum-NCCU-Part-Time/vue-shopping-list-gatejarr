<script setup>
import { ref } from 'vue'

const newListTitle = ref('')
const newListItems = ref([])

const newList() => {
  const { id, newListTitle, newListItems} = newList;
  return fetch('http://localhost:3000/lists/', {
  method: 'POST',
  headers: {"Content-Type": "application/json"},
  body: JSON.stringify({ title, items, updatedAt: new Date() })
})
.then(res => res.json())
.then(
  data => console.log(data)
  // or whatever you need to do
)
}
</script>
<template></template>
