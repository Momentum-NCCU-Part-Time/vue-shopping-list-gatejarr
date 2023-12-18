<script setup>
import { ref } from 'vue'
const newItem = ref('')
const emit = defineEmits(['itemAdded'])

const addItem = (newItem) => {
  fetch('http://localhost:3000/lists/' + newItem.value, {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ itemName: newItem.value, purchased: false })
  }).then((res) => res.json())
}
</script>

<template>
  <form id="newItemForm" @submit.prevent="addItem">
    <input v-model="newItem" type="text" placeholder="Add Item" required />
    <button type="submit">Add</button>
  </form>
</template>
