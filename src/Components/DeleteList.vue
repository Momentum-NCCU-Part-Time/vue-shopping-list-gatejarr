<script setup>
import { ref } from 'vue'

const props = defineProps({ deleteList: Object })
const emit = defineEmits(['listDeleted'])
const listDelete = ref(false)

const deleteList = (list) => {
  fetch('http://localhost:3000/lists/' + props.deleteList.id, {
    method: 'DELETE'
  })
    .then((res) => res.json())
    .then((listDeleted) => {
      emit('listDeleted', listDeleted)
    })
}

function confirmDelete(e) {
  listDelete.value = e
}
</script>

<template>
  <div class="deletePopup">
    <button v-if="listDelete" class="button" @click="confirmDelete(false)">Cancel</button>
    <button v-else class="confirmDeleteButton" @click="confirmDelete(true)">Delete</button>
    <form class="delete" v-if="listDelete" @click.prevent="deleteList">
      <h3>Are you sure you want to delete the {{ props.deleteList.title }} list?</h3>
      <button type="submit">Delete Permanently</button>
      <button v-if="listDelete" @click="confirmDelete(false)">Cancel</button>
    </form>
  </div>
</template>
