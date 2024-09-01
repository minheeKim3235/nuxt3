<template>
  <div :class="{ 'flex_row': inline }">
    <slot />
  </div>
</template>
<script setup>
import { provide } from 'vue'

const props = defineProps({
  inline: Boolean
})
const model = defineModel();

provide('radioModel', model);
provide('inline', props.inline);
</script>
<style lang="scss" scoped>
.flex_row {
  display: flex;
}
</style>

