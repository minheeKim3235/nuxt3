<template>
  <div class="radio_item">
    <input type="radio" v-model="radioModel" :value="value" :id="uniqueId">
    <label :for="uniqueId">{{ label }}</label>
  </div>
</template>
<script setup>
import { inject, ref, onMounted } from 'vue'
import { nanoid } from 'nanoid'

const props = defineProps({
  value: {
    required: true
  },
  label: String
})

const radioModel = inject('radioModel');
const uniqueId = ref();

onMounted(() => {
  uniqueId.value = nanoid(8);
})
</script>
<style lang="scss" scroped>
.radio_item {
  display: flex;
  align-items: center;
}
label {
  padding-left: 5px;
}
</style>