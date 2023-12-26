<script setup>
import { ref } from 'vue'

const props = defineProps({ list: Object })
const emit = defineEmits(['listDeleted'])

const deleteList = (list) => {
  fetch('http://localhost:3000/lists/' + props.list.id, {
    method: 'DELETE'
  })
    .then((res) => res.json())
    .then((listDeleted) => {
      emit('listDeleted', listDeleted)
    })
}
</script>

<template>
  <button @click="deleteList">Delete List</button>
</template>
