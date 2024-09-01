<template>
  <div class="input_basic" :rtl="rtl">
    <input
      :type="type"
      v-model="inputModel"
      :value="value"
      :id="uniqueId"
      :required="required"
      :placeholder="placeholder"
      :maxlength="maxLength"
      />
    <label :for="uniqueId">{{ label }}</label>
    <div class="input_options" v-if="messege || counter">
      <div class="input_messege">
        {{ messege }}
      </div>
      <div class="input_counter" v-if="counter">
        <span>{{ value.length || 0}}</span>
        <span>/{{ maxLength }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { nanoid } from 'nanoid'


const props = defineProps({
  type: String,
  value: String,
  label: String,
  required: Boolean,
  placeholder: String,
  counter: Boolean,
  maxLength: Number,
  messege: String,
  id: String,
  rtl: {
    type: Boolean,
    default: false
  }
})
const inputModel = defineModel();
const uniqueId = ref();

onMounted(() => {
  uniqueId.value = props.id || nanoid(8);
})
</script>

<style lang="scss" scoped>
.input_basic {
  display: flex;
  flex-flow: row wrap;
  input[type='text'] {
    order: 2;
    flex-grow: 1;
    & + label {
      order: 1;
      flex: 0 0 auto;
    }
  }
  &[rtl='true'] {
    flex-direction: row-reverse;
  }
}
input[type=text]{
  
  &:focus {
    outline: none;
    border: 1px solid green;
  }
  &[required] {
    border-color: red;
  }
}
.input_options {
  order: 3;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .input_counter {
    margin-left: auto;
  }
}
</style>