<script setup>
import { ref } from 'vue';

const props = defineProps(['modelValue']);
const selectedQuote = ref('');

const getRandomQuote = () => {
  if (props.modelValue.length > 0) {
    const randomIndex = Math.floor(Math.random() * props.modelValue.length);
    selectedQuote.value = props.modelValue[randomIndex];
  }
};

getRandomQuote();
</script>

<template>
  <div class="quote-display">
    <blockquote class="quote-dispay__output">
      "{{ selectedQuote || 'Цитата отсутствует' }}"
    </blockquote>
    <button @click="getRandomQuote">Показать случайную цитату</button>
  </div>
</template>

<style>
.quote-display {
  text-align: center;
}

.quote-dispay__output {
  font-size: 24px;
  font-style: italic;
  width: 600px;
  height: 150px;
}
</style>
