<template>
  <teleport to="body">
    <transition name="message-fade">
      <div v-if="visible" class="message-box-backdrop" @click="handleCancel">
        <div class="message-box" @click="stopPropagation">
          <div class="message-box-content">
            <p>{{ message }}</p>
          </div>
          <div class="message-box-footer">
            <zt-button @click="handleCancel">Cancel</zt-button>
            <zt-button @click="handleConfirm">Confirm</zt-button>
          </div>
        </div>
      </div>
    </transition>
  </teleport>
</template>

<script lang="ts" setup>
import { ref, defineProps, defineEmits } from 'vue'

// Props
const props = defineProps({
  message: String
})

// Emits
const emit = defineEmits(['update:visible', 'confirm', 'cancel'])

// Reactive state
const visible = ref(true)

// Methods
const handleConfirm = () => {
  emit('confirm')
  visible.value = false // Close the dialog
}

const handleCancel = () => {
  emit('cancel')
  visible.value = false // Close the dialog
}
const stopPropagation = (event: Event) => {
  event.stopPropagation()
}
</script>

<style scoped>
/* Add your CSS styles for MessageBox component */
.message-box-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.5);
}

.message-box {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}

.message-box-header,
.message-box-footer {
  text-align: center;
}

.message-box-content {
  margin: 20px 0;
}
</style>
