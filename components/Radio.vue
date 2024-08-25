<template>
  <div class="radio_item" :class="{ 'radio_inline': inline }">
    <input type="radio" v-model="radioModel" :value="value" :id="label">
    <label :for="label">{{ label }}</label>
  </div>
</template>
<script setup>
import { inject } from 'vue'

const props = defineProps({
  value: {
    required: true
  },
  label: String
})

const radioModel = inject('radioModel');
const inline = inject('inline');
</script>
<style lang="scss" scroped>
.radio_item {
  display: flex;
  align-items: center;
}
label {
  padding-left: 5px;
}
.radio_inline {
  margin-right: 10px;
}
</style>