<script setup>
import { ref } from 'vue'
import DeleteModal from './DeleteModal.vue'

const props = defineProps({ list: Object })
const lists = ref([])
const emit = defineEmits(['listReset'])
const showDeleteModal = ref(false)

 const resetLists = () => {
   emit('listReset', resetLists)
 }
</script>

<template>
  <ul>
    <li v-for="items in props.list.items" :key="list.items.id">
      {{ items.itemName }}
      <input v-model="purchased" type="checkbox" />
      <!-- CHECKBOX / PURCHASED WIP-->
    </li>
  </ul>
  <button @click="showDeleteModal = true">Delete List</button>
  <DeleteModal
    :deleteList="list"
    v-if="showDeleteModal"
    @list-deleted="showDeleteModal = false"
    @deleteConfirmed = 'resetLists'
    @delete-cancelled="showDeleteModal = false"
  />
</template>
