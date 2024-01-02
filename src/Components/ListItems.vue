<script setup>
import { ref } from 'vue'
import DeleteModal from './DeleteModal.vue'

const props = defineProps({ list: Object })
const emit = defineEmits(['listReset'])
const showDeleteModal = ref(false)

const resetLists = () => {
  emit('listReset', resetLists)
}

const purchased = (items) => {
  items.purchased = !items.purchased
  itemPurchased(props.list)
}

const itemPurchased = (list) => {
  fetch('http://localhost:3000/lists/' + props.list.id, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: props.list.title,
      items: [...props.list.items],
      updatedAt: new Date()
    })
  }).then((res) => res.json())
}
</script>

<template>
  <ul>
    <li
      v-for="items in props.list.items"
      :key="list.items.id"
      @click="purchased(items)"
      :class="{ strikeThrough: items.purchased }"
    >
      {{ items.itemName }}
      <input v-model="items.purchased" type="checkbox" />
    </li>
  </ul>
  <button @click="showDeleteModal = true">Delete List</button>
  <DeleteModal
    :deleteList="list"
    v-if="showDeleteModal"
    @list-deleted="showDeleteModal = false"
    @deleteConfirmed="resetLists"
    @delete-cancelled="showDeleteModal = false"
  />
</template>

<style>
.strikeThrough {
  text-decoration: line-through;
}

ul {
  font-family: 'Courier New', Courier, monospace;
}
</style>
