<template>
  <button
    class="zt-button"
    @click="handleClick"
    :disabled="buttonDisabled || loading"
    :autofocus="autofocus"
    :type="nativeType"
    :class="[
      type ? 'el-button--' + type : '',
      buttonSize ? 'el-button--' + buttonSize : '',
      {
        'is-disabled': buttonDisabled,
        'is-round': round
      }
    ]"
  >
    <i class="el-icon-loading" v-if="loading"></i>
    <i :class="icon" v-if="icon && !loading"></i>
    <!--通过$slots.default 获取所有没有被包含在具名插槽中的节点，这里指el-button标签中所包裹的所有内容-->
    <span v-if="$slots.default"><slot></slot></span>
  </button>
</template>

<script setup>
import { ref } from 'vue'
defineOptions({
  name: 'TButton'
})
const props = defineProps({
  modelValue: {
    type: [String, Number],
    default: ''
  },
  disabled: {
    type: Boolean,
    default: false
  },
  size: {
    type: String,
    default: 'medium',
    validator: (value) => ['small', 'medium', 'large'].includes(value)
  },
  nativeType: {
    // 原生 type 属性
    type: String,
    default: 'button'
  },
  round: {
    type: Boolean,
    default: false
  }
})
const emit = defineEmits(['update:modelValue', 'change', 'focus', 'blur'])

const inputValue = ref(props.value)

const handleInput = (event) => {
  inputValue.value = event.target.value
  emit('update:modelValue', inputValue.value)
}

const handleChange = (event) => {
  emit('change', event.target.value)
}

const handleFocus = (event) => {
  emit('focus', event)
}

const handleBlur = (event) => {
  emit('blur', event)
}
</script>
