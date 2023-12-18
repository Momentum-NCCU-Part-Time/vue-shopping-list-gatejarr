<script setup>
import { ref } from 'vue'

const newListTitle = ref('')
const newListItems = ref([])

const newList = {
  title: this.newListTitle,
  items: this.newList.items.map((item) => ({
    itemName: item.name,
    purchased: false
  }))
}
fetch('http://localhost:3000/lists/', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify(newList)
})
  .then((res) => res.json())
  .then((data) => {
    this.emit('listAdded', data)
  })
</script>
<template></template>
