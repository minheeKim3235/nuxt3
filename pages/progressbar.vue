<template>
  <div>
    <TabGroups ref="nowTab">
      <TabItem title="탭 1" :slide-to="['#pos1', 'tab_content']"></TabItem>
      <TabItem title="탭 2" :slide-to="['#pos2', 'tab_content']" ref="ii"></TabItem>
      <TabItem title="탭 3" :slide-to="['#pos3', 'tab_content']"></TabItem>
    </TabGroups>

    <div id="tab_content">
      
      <ObserverTrigger @on-viewport="test" id="pos1">
        탭 1
      </ObserverTrigger>
      
      <ObserverTrigger @on-viewport="test" id="pos2">
        탭 2
      </ObserverTrigger>
      <ObserverTrigger @on-viewport="test" id="pos3">
        탭 3
      </ObserverTrigger>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const nowTab = ref(null)
const ii = ref(null)

const test = (el) => {
  console.log(el.target);
  nowTab.value.changeActive(ii.value.tabId);
}
const onScroll = () => {
  console.log('hi');
}
onMounted(() => {
  //console.log(ii.value.tabId);
  nowTab.value.changeActive(ii.value.tabId);
})
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