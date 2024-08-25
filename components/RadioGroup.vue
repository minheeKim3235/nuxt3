<template>
  <div :class="{ 'flex_row': inline }">
    <slot />
  </div>
</template>
<script setup>
import { computed, provide } from 'vue'

const props = defineProps({
  modelValue: {
    required: true
  },
  inline: Boolean
})

const emit = defineEmits(['update:modelValue'])

provide('radioModel', computed({
  get () {
    return props.modelValue
  },
  set (value) {
    emit('update:modelValue', value)
  }
}));

provide('inline', props.inline);
</script>
<style lang="scss" scoped>
.flex_row {
  display: flex;
}
</style>

