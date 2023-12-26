<script setup>
import { ref } from 'vue'

const newList = ref('')
const emit = defineEmits(['newListCreated'])

const createNewList = () => {
  fetch('http://localhost:3000/lists/', {
    method: 'POST',
    headers: { 'Content-type': 'application/json' },
    body: JSON.stringify({
      title: newList.value,
      items: [],
      updatedAt: new Date()
    })
  })
    .then((res) => res.json())
    .then((newList) => {
      emit('newListCreated', newList)
      resetLists()
    })
}

const resetLists = () => {
  newList.value = ''
}
</script>

<template>
  <div id="newListForm">
    <form @submit.prevent="createNewList">
      <input v-model="newList" type="text" placeholder="Store Name" required />
      <button type="submit" id="saveNewList">New List</button>
    </form>
  </div>
</template>
