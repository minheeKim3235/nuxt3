<template>
  <div class="tab_basic">
    <ul class="tab_list">
      <li
        v-for="(tab, index) in tabs"
        :key="tab.title"
        :id="tab.tabId"
        :class="{ on: activeTab === tab.tabId }"
        @click="activateTab(tab)"
      >
        <a :href="tab.link?.url" :target="tab.link?.target" v-if="tab.link">{{ tab.title }}</a>
        <button type="button" v-else>{{ tab.title }}</button>
      </li>
    </ul>
    <slot></slot> <!-- Allow dynamic content to be injected -->
    <slot name="slide"></slot>
  </div>
</template>

<script setup>
import { ref, provide, defineEmits, nextTick, defineExpose, onMounted, onUnmounted } from 'vue';

const activeTab = ref('');
const tabs = ref([]);
const emit = defineEmits(['slideActive']);
let observers = [];

// Provide tab management methods to child components
provide('addTab', (tab) => {
  const count = tabs.value.push(tab);
  if (count === 1) {
    activeTab.value = tab.tabId; // Automatically set the first tab as active
  }
});
provide('activeTab', activeTab);

const changeActive = (val) => {
  activeTab.value = val;
};

const activateTab = async (tab) => {
  changeActive(tab.tabId); // Update active tab
  emit('slideActive', tab.slideTo); // Emit the slideActive event

  await nextTick();

  if (tab.slideTo) {
    const targetElement = document.querySelector(tab.slideTo[0]);
    window.scrollTo({ top: targetElement.offsetTop, behavior: 'smooth' });
  }
};

// IntersectionObserver callback
const handleIntersection = (entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      const matchedTab = tabs.value.find(tab => tab.slideTo && tab.slideTo[0] === `#${entry.target.id}`);
      if (matchedTab) {
        changeActive(matchedTab.tabId);
      }
    }
  });
};

// Initialize observers
const initObservers = () => {
  observers.forEach(observer => observer.disconnect()); // Clear previous observers
  observers = [];

  tabs.value.forEach(tab => {
    if (tab.slideTo) {
      const targetElement = document.querySelector(tab.slideTo[0]);
      if (targetElement) {
        const observer = new IntersectionObserver(handleIntersection, {
          threshold: 0.5, // Adjust this value based on when you want the tab to activate
        });
        observer.observe(targetElement);
        observers.push(observer);
      }
    }
  });
};

onMounted(() => {
  initObservers();
});

onUnmounted(() => {
  observers.forEach(observer => observer.disconnect()); // Clean up observers
});

defineExpose({
  changeActive,
  initObservers
});
</script>

<style lang="scss" scoped>
.tab_basic {
  display: sticky;
  top: 0;
  .tab_list {
    display: flex;
    li {
      flex-grow: 1;
      border: 1px solid #ddd;
      a, button {
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 10px 0;
        width: 100%;
        height: 100%;
        background-color: #fff;;
        box-sizing: border-box;
      }
      &.on {
        a, button {
          color: #fff;
          background: #555;
        }
        }
    }
  }
}
</style>