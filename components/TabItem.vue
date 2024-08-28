<template>
  <div class="tab_content" v-show="isActive">
    <slot></slot>
  </div>
</template>

<script setup>
import { inject, onBeforeMount, watch } from "vue";
import { nanoid } from 'nanoid'

const props = defineProps({
  title: String,
  tabId: String,
  slideTo: String,
  link: Object
});

const tabId = ref("");
const isActive = ref(false);
const addTab = inject("addTab");
const activeTab = inject("activeTab");

onBeforeMount(() => {
  if (props.slideTo || props.tabId) {
    tabId.value = props.tabId
  } else {
    tabId.value = nanoid(8);
  }

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
</script>

<style lang="scss" scoped>

</style>