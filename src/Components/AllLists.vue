<script setup>
import { ref } from 'vue'
import AddItem from './AddItem.vue'
import ListItems from './ListItems.vue'
import NewList from './NewList.vue'
import DeleteList from './DeleteList.vue'

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
      <DeleteList :list="list" @list-deleted="getLists" />
      <AddItem :list="list" @item-added="getLists" />
    </div>
    <div>
      <ListItems :list="list" />
    </div>
  </div>
</template>
