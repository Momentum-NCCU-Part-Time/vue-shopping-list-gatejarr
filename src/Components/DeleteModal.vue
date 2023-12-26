<script>
import { ref } from 'vue'
import ConfirmDialogue from './ConfirmDialogue.vue'

export default {
  components: { ConfirmDialogue },
  methods: {
    async confirmDelete() {
      const ok = await this.$refs.confirmDialogue.show({
        title: 'Delete List',
        message: 'Are you sure you want to delete this list?',
        okButton: 'Delete Forever'
      })
      if (ok) {
        alert('You have successfully deleted this list.')
      }
    }
  }.then deleteList()
}

const props = defineProps({ list: Object })
const emit = defineEmits(['listDeleted'])

const deleteList = (list) => {
  fetch('http://localhost:3000/lists/' + props.list.id, {
    method: 'DELETE'
  })
    .then((res) => res.json())
    .then((listDeleted) => {
      emit('listDeleted', listDeleted)
    })
}
</script>

<template>
  <div>
    <h1>Delete List</h1>
    <button class="delete-btn" @click="confirmDelete">DeleteModal</button>
    <confirm-dialog ref="confirmDialogue"></confirm-dialog>
  </div>
</template>
