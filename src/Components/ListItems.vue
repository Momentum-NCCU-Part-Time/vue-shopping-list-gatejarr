<script setup>
import { ref } from 'vue'
import DeleteModal from './DeleteModal.vue'

const props = defineProps({ list: Object })
const lists = ref([])
const showDeleteModal = ref(false)

const getLists = () => {
  fetch('http://localhost:3000/lists/', {
    method: 'GET',
    headers: { 'Content-type': 'application/json' }
  })
    .then((res) => res.json())
    .then((data) => (lists.value = data))
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
    @delete-cancelled="showDeleteModal = false"
  />
</template>
