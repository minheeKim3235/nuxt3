<template>
  <div>
    <TabGroups ref="nowTab">
      <TabItem title="탭 1" :slide-to="['#pos1', 'tab_content']"></TabItem>
      <TabItem title="탭 2" :slide-to="['#pos2', 'tab_content']"></TabItem>
      <TabItem title="탭 3" :slide-to="['#pos3', 'tab_content']"></TabItem>
    </TabGroups>

    <div id="tab_content">
      
      <div id="pos1">
        탭 1
      </div>
      
      <div id="pos2">
        탭 2
      </div>
      <div id="pos3">
        탭 3
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const nowTab = ref(null)
</script>

<style lang="scss" scoped>
.tab_basic {
  position: sticky;
  top: 0;
}
div[id^='pos'] {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 800px;
  background:thistle;
}
#pos2 {
  background: lavender;
}
</style>