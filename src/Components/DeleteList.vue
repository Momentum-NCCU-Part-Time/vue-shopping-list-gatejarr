<script setup>
import { ref } from 'vue'

const props = defineProps({ deleteList: Object })
const emit = defineEmits(['listDeleted'])

const deleteList = (list) => {
  fetch('http://localhost:3000/lists/' + props.deleteList.id, {
    method: 'DELETE'
  })
    .then((res) => res.json())
    .then((listDeleted) => {
      emit('listDeleted', listDeleted)
    })
}
</script>

<template>
  <button @click="deleteList">Delete NO CONIRM</button>
</template>
