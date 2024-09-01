<template>
  <div>
    <Accordion snap>
      <template v-for="(item, i) in rules" :key="i" >
        <AccordionItem  :title="item.title" :index="i" :expanded="item.expanded">
          {{ item.items }}
        </AccordionItem>
      </template>
    </Accordion>
    <TabGroups class="unionTab" @slide-active="unionShow">
      <TabItem title="tab1">content 1</TabItem>
      <TabItem title="모집안내" :slideTo="['#pos1','union']"></TabItem>
      <TabItem title="수업안내" :slideTo="['#pos2','union']"></TabItem>
      <TabItem title="생활안내" :slideTo="['#pos3','union']"></TabItem>
      <TabItem title="tab5">content 3</TabItem>
    </TabGroups>
    <div v-show="isShow === 'union'">
      <TabGroups class="unionSubTab">
        <TabItem title="sub11" :slideTo="['#sub11', 'union']"></TabItem>
        <TabItem title="sub12" :slideTo="['#sub12', 'union']"></TabItem>
        <TabItem title="sub13" :slideTo="['#sub13', 'union']"></TabItem>
      </TabGroups>
      <div id="pos1" >
        모집안내
        <div id="sub11" style="height: 800px; background: wheat">
          sub11
        </div>
        <div id="sub12" style="height: 800px; background: ghostwhite">
          sub12
        </div> 
        <div id="sub13" style="height: 800px; background: wheat">
          sub13
        </div>
      </div>
      <div id="pos2"  style="height: 800px; background: ghostwhite">
        수업안내
      </div>
      <div id="pos3"  style="height: 800px; background: wheat">
        생활안내
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
  if (el) {
    isShow.value = el[1]
  } else {
    isShow.value = ''
  }
}
onMounted(() => {
  
})
</script>

<style lang="scss" scoped>
div[id^='pos'] {
  display: flex;
  flex-flow: column wrap;
  justify-content: center;
  align-items: center;
  width: 100%;
}
div[id^='sub'] {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.accordion_item {
  margin-bottom: -1px;
}
.unionTab {
  position: sticky;
  top: 0;
}
.unionSubTab {
  position: sticky;
  top: 35px;
}
</style>