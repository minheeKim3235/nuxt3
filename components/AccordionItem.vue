<template>
  <div class="accordion_item">
    <button class="accordion_header" :class="{'is_open': isActive === true }" @click="toggle">
      <div v-if="$slots.title">
        <slot name="title"></slot>
      </div>
      <span v-else>{{ title }}</span>
    </button>
    <transition name="acc"
      @before-enter="beforeEnter"
      @enter="enter"
      @before-leave="beforeLeave"
      @leave="leave"
    >
      <div class="accordion_content" :class="{'accordion_expanded': isActive === true, 'snap_motion': snap}" v-show="isActive === true">
        <slot></slot>
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref, inject, computed, onMounted } from 'vue';

const props = defineProps({
  title: String,
  index: [Number, String], // index prop을 추가하여 아이템의 인덱스를 추적합니다.
  expanded: {
    type: Boolean,
    default: false
  }
});

const multiple = inject('multiple');
const snap = inject('snap');
const activeIndex = inject('activeIndex');
const setActiveIndex = inject('setActiveIndex');

const isActive = computed(() => {
  if (!multiple) {
    return activeIndex.value === props.index;
  } else {
    return activeIndex.value.includes(props.index);
  }
});

// methods
const toggle = () => {
  if (!multiple) {
    setActiveIndex(props.index);
  } else {
    if (isActive.value) {
      activeIndex.value = activeIndex.value.filter(i => i !== props.index);
    } else {
      activeIndex.value.push(props.index);
    }
  }
}

const beforeEnter = (el) => {
  el.style.height = '0';
}
const enter = (el) => {
  el.style.height = el.scrollHeight + 'px';
}
const beforeLeave = (el) => {
  el.style.height = el.scrollHeight + 'px';
}
const leave = (el) => {
  el.style.height = '0';
}

onMounted(() => {
  if (props.expanded) {
    if (!multiple) {
      setActiveIndex(props.index);
    } else {
      isActive.value = true;
    }
  }
});

</script>

<style lang="scss" scoped>
.accordion_item {
  width: 100%;
}
.accordion_header {
  position: relative;
  display: block;
  padding: 0 0 0 30px;
  width: 100%;
  font-size: 22px;
  color: #222;
  line-height: 68px;
  text-align: left;
  border: 1px solid #d3d3d3;
  box-sizing: border-box;

  &:before {
    content: '';
    position: absolute;
    right: 30px;
    top: 50%;
    width: 1px;
    height: 23px;
    background: #d5d5d5;
    margin: -11px 11px 0 0;
  }
  
  &:after {
    content: '';
    position: absolute;
    right: 30px;
    top: 50%;
    width: 23px;
    height: 1px;
    background: #d5d5d5;
  }

  &.is_open {
    &:before {
      display: none;
    }
    &:after {
      background: #5c5c5c;
    }
  }
}
.accordion_content {
  overflow: hidden;
  &.accordion_expanded {
    height: auto;
  }
  &.snap_motion {
    transition: 150ms ease-out;
  }
}
</style>
