<template>
  <div ref="observerElement">
    <slot></slot>
  </div>
</template>

<script setup>
import { ref, onMounted, defineEmits } from 'vue'

const props = defineProps({
  options: Object,
  default: {
    root: null,
    rootMargin: '0px',
    threshold: 1
  }
})
const observerElement = ref(null);
const emit = defineEmits(['onViewport'])
let handleIntersect = (target) => {
  emit('onViewport', target)
}

onMounted(() => {
  new IntersectionObserver((entries) => {
    if ( entries[0].isIntersecting ) {
      handleIntersect(entries[0])
    }
  }, props.options).observe(observerElement.value)
})
</script>

<style lang="scss" scoped>

</style>