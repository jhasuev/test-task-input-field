<template>
  <div class="text-field">
    <div class="text-field__label">{{ label }}</div>

    <div
      class="text-field__field-wrapper"
      :class="{ error: isLimitExceeded }"
    >
      <textarea
        class="text-field__field"
        :class="{ filled: modelValue.length }"
        :value="modelValue"
        @input="emits('update:modelValue', $event.target.value)"
      ></textarea>
      <span class="text-field__placeholder">{{ placeholder }}</span>
      <i class="text-field__preloader"></i>
    </div>
    
    <div class="text-field__footer">
      <div v-if="isLimitExceeded" class="text-field__error">Ошибка</div>
      <div class="text-field__counter">{{ modelValue.length }}/1000</div>
      <a
        href="javascript:void(0)"
        class="text-field__clear"
        @click="emits('update:modelValue', '')"
      >Очистить</a>
    </div>
  </div>
</template>

<script setup>
import {
  defineOptions,
  defineProps,
  defineEmits,
  computed,
} from 'vue'

defineOptions({ name: 'TextField' })
const props = defineProps({
  modelValue: {
    type: String,
    default: '',
  },
  label: {
    type: String,
    default: 'Текст перед полем ввода',
  },
  placeholder: {
    type: String,
    default: 'Название поля',
  },
});
const emits = defineEmits(['update:modelValue'])

const isLimitExceeded = computed(() => props.modelValue.length >= 1000)

</script>

<style scoped>

.text-field {
  font-family: 'Roboto', sans-serif;
}

.text-field__label {
  margin-bottom: 4px;
  color: #303030;
  font-size: 18px;
  font-weight: 500;
  letter-spacing: 0.03px;
}

.text-field__field-wrapper {
  position: relative;
  width: 100%;
  max-width: 326px;
  margin-bottom: 8px;


  padding: 24px 0 10px 12px;
  background-color: #F0F0F0;
  border-radius: 8px;
}

.text-field__field-wrapper.error {
  background-color: #FBF0EF;
}

.text-field__field {
  display: block;
  width: 100%;
  min-height: 146px;
  padding-right: 4px;
  
  border: none;
  outline: none;
  resize: none;
  background-color: transparent;

  color: #4F4F4F;
  font-size: 16px;
  line-height: 22px;
  letter-spacing: 0.02px;
  box-sizing: border-box;
}

.text-field__field::-webkit-scrollbar {
  width: 3px;
}

.text-field__field::-webkit-scrollbar-track {
  background-color: transparent;
}

.text-field__field::-webkit-scrollbar-thumb {
  box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.2);
}

.text-field__placeholder {
  position: absolute;
  left: 12px;
  right: 32px;
  top: 4px;

  color: #878F97;
  font-size: 16px;
  font-family: Roboto;
  font-weight: 400;
  line-height: 22px;
  letter-spacing: 0.02px;

  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;

  transition: font-size .3s;
}

.text-field__field.filled ~ .text-field__placeholder,
.text-field__field:focus ~ .text-field__placeholder {
  font-size: 12px;
}

.text-field__preloader {
  position: absolute;
  top: 4px;
  right: 4px;
  border: 2px solid #00B6D0;
  border-right-color: transparent;
  width: 24px;
  height: 24px;
  border-radius: 50%;

  animation: spin 1s infinite linear;
  opacity: 0;
  transition: opacity .3s;
}

/* не понял, когда должен появляться прелодер, сделал так... */
.text-field__field:focus ~ .text-field__preloader {
  opacity: 1;
}

@keyframes spin {
  from {transform:rotate(0deg);}
  to {transform:rotate(360deg);}
}

.text-field__footer {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 3px;

  font-size: 14px;
  letter-spacing: 0.04px;
}

.text-field__error {
  color: #D6675C;
}

.text-field__counter {
  color: #878F97;
}

.text-field__clear {
  color: #00B6D0;
  text-decoration: none;
}

</style>
