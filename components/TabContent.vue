<template>
  <div class="tab_content">
    <slot></slot>
  </div>
</template>

<script setup>
import { inject } from 'vue'

const props = defineProps({
  slideTab: Boolean
})

const addContent = inject('addContent')
</script>

<style lang="scss" scoped>

</style>