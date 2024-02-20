<script setup>
import { ref } from 'vue'

const newItem = ref('')
const newItemQuant = ref('')
const props = defineProps({ list: Object })
const emit = defineEmits(['itemAdded'])

const addItem = () => {
  fetch('http://localhost:3000/shoppinglists/' + props.list._id + '/items', {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: props.list.title,
      items: [
        ...props.list.items,
        {
          name: newItem.value,
          quantity: newItemQuant.value,
          purchased: false
        }
      ],
      updatedAt: new Date()
    })
  })
    .then((res) => res.json())
    .then((addedItem) => {
      emit('itemAdded', addedItem)
      resetItem()
    })
}

const resetItem = () => {
  newItem.value = ''
  newItemQuant.value = ''
}
</script>

<template>
  <form id="newItemForm" @submit.prevent="addItem">
    <input v-model="newItem" type="text" placeholder="Add Item" required />
    <input v-model="newItemQuant" type="number" placeholder="Quantity?" />
    <button type="submit">Add</button>
  </form>
</template>
