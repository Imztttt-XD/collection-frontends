<script lang="ts" setup>
import { ref } from 'vue'
import MessageBox from '../packages/components/MessageBox/MessageBox.vue'
const dialogVisible = ref(false)

const handleClose = (done: () => void) => {
  console.log('1111')

  // .then(() => {
  //   done()
  // })
  // .catch(() => {
  //   // catch error
  // })
}
</script>

<template>
  <zt-button type="primary" @click="dialogVisible = true">按钮</zt-button>
  <zt-dialog v-model="dialogVisible" title="Tips" :before-close="handleClose">
    <span>This is a message</span>
    <template #footer>
      <div class="dialog-footer">
        <zt-button @click="dialogVisible = false" size="small">Cancel</zt-button>
        <zt-button type="primary" @click="dialogVisible = false" size="small"> Confirm </zt-button>
      </div>
    </template>
  </zt-dialog>
</template>

<style scoped></style>
