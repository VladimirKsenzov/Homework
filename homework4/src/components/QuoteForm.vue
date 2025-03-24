<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

const newQuote = ref('');

const submitQuote = () => {
  const trimedNewQuote = newQuote.value.trim();
  if (trimedNewQuote !== '') {
    const updatedQuotes = [...props.modelValue, trimedNewQuote];
    emit('update:modelValue', updatedQuotes);
    newQuote.value = '';
  }
};
</script>

<template>
  <form class="quote-form" @submit.prevent="submitQuote">
    <label for="quote">Введите новую цитату:</label>
    <textarea
      id="quote"
      class="quote-form__input"
      v-model="newQuote"
      placeholder="Введите новую цитату..."
      required
    ></textarea>
    <button type="submit" class="quote-form__btn">Добавить цитату</button>
  </form>
</template>

<style scoped>
.quote-form {
  margin: 16px 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.quote-form__input {
  width: 90%;
  height: 100px;
  padding: 10px;
  font-size: 20px;
  border-radius: 8px;
  border: 1px solid #fff;
  background: transparent;
  resize: none;
}

.quote-form__btn {
  width: 160px;
  padding: 10px 10px;
  font-size: 16px;
  border-radius: 8px;
  text-align: center;
}
</style>
