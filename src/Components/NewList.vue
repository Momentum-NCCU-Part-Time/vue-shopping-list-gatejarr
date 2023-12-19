<script setup>
import { ref } from 'vue'

const newList = ref('')
const newListTitle = ref('')
const newListItems = ref([])

const createNewList = () => {
  fetch('http://localhost:3000/lists/', {
    method: 'POST',
    headers: { 'Content-type': 'application/json' },
    body: JSON.stringify({
      title: newListTitle.value,
      items: newListItems.value,
      updatedAt: new Date()
    })
  })
    .then((res) => res.json())
    .then((lists) => lists)
}
</script>
<template>
  <div id="newListForm">
    <form @submit.prevent="createNewList">
      <input
        v-model.trim="newListTitle"
        type="text"
        id="newListTitle"
        placeholder="Store Name"
        required
      />
      <input
        v-model.trim="newListItems"
        type="text"
        id="newListItems"
        placeholder="Items"
        required
      />
      <button type="submit" id="saveNewList">Save</button>
    </form>
  </div>
</template>
