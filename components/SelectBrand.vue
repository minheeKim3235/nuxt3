<template>
  <div class="select_brand">
    <RadioGroup v-model="model" inline>
      <Radio v-for="(brand, i) in useBrands" :value="brand.value" :label="brand.label"></Radio>
    </RadioGroup>
  </div>
</template>

<script setup>
import { ref, computed, defineModel } from 'vue';

const props = defineProps({
  items: Array
})
const model = defineModel();

const brands = ref([
  { value: 'CSnormal', label: '청솔' },
  { value: 'CSneo', label: '청솔네오' },
  { value: 'HPnormal', label: '강하' }
]);

const useBrands = computed(() => { 
  return brands.value.filter(item => props.items.includes(item.label));
})
// onMounted(() => {
//   selectBrand.value = useBrands.value[0].value;
// })
</script>

<style lang="scss" scoped>
.select_brand {
  position: fixed;
  bottom: 10px;
  display: inline-flex;
  margin-left: 10px;
  padding: 10px 15px;
  background: #fff;
  border-radius: 8px;
  box-shadow: 1px 1px 5px rgba(0,0,0,.15);
  z-index: 20;
}
</style>