<script setup>
import { ref } from 'vue'
const newItem = ref('')
const props = defineProps({itemProp: Object, list: Object})
// const existingItems = ref(props.list[items])

const addItem = () => {
  fetch('http://localhost:3000/lists/' + props.list.id, {
    method: 'PATCH',
    headers: {'Content-Type': 'application/json'},
    body: JSON.stringify({
      title: props.list.title,
      items: props.list.items.push({
        id: props.itemProp.id,
        itemName: newItem.value,
        purchased: 'false'
      }),
      updatedAt: new Date ()
    })
  })
  .then((res) => res.json())
}
</script>

<template>
  <form id="newItemForm" @submit.prevent="addItem">
    <input v-model="newItem" type="text" placeholder="Add Item" required />
    <button type="submit">Add</button>
  </form>
</template>
