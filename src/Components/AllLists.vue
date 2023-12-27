<script setup>
import { computed, ref } from 'vue'
import dayjs from 'dayjs'
import AddItem from './AddItem.vue'
import ListItems from './ListItems.vue'
import NewList from './NewList.vue'
import DeleteList from './DeleteList.vue'
//import DeleteModal from './DeleteModal.vue'

const lists = ref([])
const purchased = ref(false)

// const newItem = ref('')

fetch('http://localhost:3000/lists/', {
  method: 'GET',
  headers: { 'Content-type': 'application/json' }
})
  .then((res) => res.json())
  .then((data) => (lists.value = data))

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
  <div>
    <NewList @new-list-created="getLists" />
  </div>
  <div v-for="list in lists" :key="list.id">
    <div>
      <h2>{{ list.title }}</h2>
      <p>Updated At: {{ dayjs(list.updatedAt).format('MMMM D, YYYY h:mm A') }}</p>
      <!-- <button @click="showDeleteModal = true">DeleteModal</button>
      <DeleteModal :list="list" v-if="showDeleteModal" /> -->
      <DeleteList :deleteList="list" @list-deleted="getLists" />
      <AddItem :list="list" @item-added="getLists" />
    </div>
    <div>
      <ListItems :list="list" />
    </div>
  </div>
</template>
