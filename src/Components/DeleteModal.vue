<script setup>
import { ref } from 'vue'

const props = defineProps({ deleteList: Object })
const emit = defineEmits(['listDeleted', 'deleteCancelled', 'deleteConfirmed'])
const listDelete = ref(false)
const lists = ref([])

const deleteList = (list) => {
  fetch('http://localhost:3000/lists/' + props.deleteList.id, {
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
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.popup-modal {
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 0.5rem;
  display: flex;
  align-items: center;
  z-index: 1;
}

.window {
  background: #fff;
  border-radius: 5px;
  box-shadow: 2px 4px 8px rgba(0, 0, 0, 0.2);
  max-width: 480px;
  margin-left: auto;
  margin-right: auto;
  padding: 1rem;
}
</style>
