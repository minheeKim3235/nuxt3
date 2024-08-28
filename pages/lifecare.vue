<template>
  <div>
    <Accordion snap>
      <template v-for="(item, i) in rules" :key="i" >
        <AccordionItem  :title="item.title" :index="i" :expanded="item.expanded">
          {{ item.items }}
        </AccordionItem>
      </template>
    </Accordion>
    <TabGroups @slide-active="unionShow">
      <TabItem title="tab1">content 1</TabItem>
      <TabItem title="tab2" slideTo="#union" tabId="union" ></TabItem>
      <TabItem title="tab3" slideTo="#union2" tabId="union"></TabItem>
      <TabItem title="tab4" slideTo="#union3" tabId="union"></TabItem>
      <TabItem title="tab5">content 3</TabItem>
    </TabGroups>
    <div v-show="isShow === 'union'">
      <div id="union" >
        union1<br />union1<br />union1<br />union1<br />union1<br />union1<br />union1<br />union1<br />union1<br />union1<br />union1<br />union1<br />union1<br />union1<br />union1<br />union1<br />
      </div>
      <div id="union2" >
        union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />union2<br />
      </div>
      <div id="union3" >
        union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />union3<br />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const isShow = ref('')
const rules = ref([
  { title: '학원생활규정', items: 'content', expanded: true },
  { title: '학원생활수칙 주요사항 안내', items: 'content', expanded: false },
  { title: '안내2', items: 'content', expanded: false },
  { title: '안내3', items: 'content', expanded: false },
])

const unionShow = (el) => {
  isShow.value = el === 'union' ? el : ''
  console.log(isShow.value)
}
</script>

<style lang="scss" scoped>
.accordion_item {
  margin-bottom: -1px;
}
</style>