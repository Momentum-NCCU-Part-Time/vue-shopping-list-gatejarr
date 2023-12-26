<script setup>
import { ref } from 'vue'

const props = defineProps({ list: Object })
</script>

<template>
  <ul>
    <li v-for="items in props.list.items" :key="list.items.id">
      {{ items.itemName }}
      <input v-model="purchased" type="checkbox" />
      <!-- CHECKBOX / PURCHASED WIP-->
    </li>
  </ul>
</template>
