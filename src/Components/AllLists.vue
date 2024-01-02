<script setup>
import { ref } from 'vue'
import dayjs from 'dayjs'
import AddItem from './AddItem.vue'
import ListItems from './ListItems.vue'
import NewList from './NewList.vue'

const lists = ref([])

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
  <br />
  <div v-for="list in lists" :key="list.id" class="listContainer">
    <div>
      <h2>{{ list.title }}</h2>
      <h3>Number of Items: {{ list.items.length }}</h3>
      <p>Updated At: {{ dayjs(list.updatedAt).format('MMMM D, YYYY h:mm A') }}</p>
      <AddItem :list="list" @item-added="getLists" />
    </div>
    <div>
      <ListItems :list="list" @list-reset="getLists" />
    </div>
  </div>
</template>

<style scoped>
h2,
h3 {
  background-color: gray;
  color: whitesmoke;
  width: 250px;
  height: auto;
}

.listContainer {
  display: flex;
  border: 1px solid black;
  min-width: 10px;
  background-color: darkgray;
  color: whitesmoke;
}
</style>
