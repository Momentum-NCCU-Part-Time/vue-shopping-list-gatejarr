<script setup>
import { ref } from 'vue'

const props = defineProps({ deleteList: Object })
const emit = defineEmits(['listDeleted', 'deleteCancelled', 'deleteConfirmed'])

const deleteList = () => {
  fetch('http://localhost:3000/shoppinglists/' + props.deleteList._id, {
    method: 'DELETE'
  })
    .then((res) => res.json())
    .then((listDeleted) => {
      emit('listDeleted', listDeleted)
      deleteConfirmed()
    })
}

const deleteConfirmed = () => {
  emit('deleteConfirmed', deleteConfirmed)
}

const cancelDelete = () => {
  emit('deleteCancelled', cancelDelete)
}
</script>

<template>
  <div class="delete-modal">
    <div class="window">
      <h3>Are you sure you want to delete {{ props.deleteList.title }}?</h3>
      <button @click="deleteList">Delete</button>
      <button @click="cancelDelete">Cancel</button>
    </div>
  </div>
</template>

<style scoped>
.window {
  background: #fff;
  border-radius: 5px;
  box-shadow: 2px 4px 8px rgba(0, 0, 0, 0.2);
  max-width: 480px;
  margin-left: auto;
  margin-right: auto;
  padding: 1rem;
  color: black;
  font-family: 'Courier New', Courier, monospace;
}
</style>
