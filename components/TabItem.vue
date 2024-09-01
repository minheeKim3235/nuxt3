<template>
  <div class="tab_content" v-show="isActive" v-if="$slots.default">
    <slot></slot>
  </div>
</template>

<script setup>
import { inject, onBeforeMount, watch, defineExpose } from "vue";
import { nanoid } from 'nanoid'

const props = defineProps({
  title: String,
  tabId: String,
  slideTo: [Array],
  link: Object
});

const tabId = ref("");
const isActive = ref(false);
const addTab = inject("addTab");
const activeTab = inject("activeTab");

onBeforeMount(() => {
  tabId.value = nanoid(8);

  addTab({
    title: props.title,
    tabId: tabId.value,
    slideTo: props.slideTo,
    link: props.link
  });
});

watch(activeTab, () => {
  isActive.value = activeTab.value === tabId.value;
});

defineExpose({
  tabId
})
</script>

<style lang="scss" scoped>

</style>