<template>
  <div class="accordion_basic">
    <slot></slot>
  </div>
</template>

<script setup>
import { ref, provide } from 'vue';

// props
const props = defineProps({
  multiple: {
    type: Boolean,
    default: false
  },
  snap: {
    type: Boolean,
    default: false
  }
});

// data
const activeIndex = ref(props.multiple ? [] : null); // 다중 선택 지원

provide('multiple', props.multiple);
provide('snap', props.snap);
provide('activeIndex', activeIndex);
provide('setActiveIndex', (index) => {
  if (props.multiple) {
    if (activeIndex.value.includes(index)) {
      activeIndex.value = activeIndex.value.filter(i => i !== index);
    } else {
      activeIndex.value.push(index);
    }
  } else {
    activeIndex.value = activeIndex.value === index ? null : index;
  }
});
</script>


<style lang="scss" scoped>
</style>
