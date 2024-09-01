<template>
  <div>
    <CustomInput type="text" v-model="testText" :value="testText" label="이름" placeholder="test" counter :max-length="30" messege="입력하세요"/>
    {{ testText }}
    <CustomInput type="checkbox" v-model="checkVal" label="체크박스1" value="val1" id="bulabula" rtl />
    <CustomInput type="checkbox" v-model="checkVal" label="체크박스2" value="val2" />
    <CustomInput type="checkbox" v-model="checkVal" label="체크박스3" value="val3" />
    {{ checkVal }}
    <RadioGroup v-model="testVal">
      <Radio value="val1" label="라디오1" />
      <Radio value="val2" label="라디오2" />
      <Radio value="val3" label="라디오3" />
      <Radio value="val4" label="라디오4" />
    </RadioGroup>
    {{ testVal }}
  </div>
</template>

<script setup>
import { ref } from 'vue'

const testVal = ref('val1');
const checkVal = ref(['val1']);
const testText = ref('');
</script>

<style lang="scss" scoped>

</style>