<script setup>
import { ref } from 'vue';
import QuoteList from './components/QuoteList.vue';
import QuoteForm from './components/QuoteForm.vue';
import QuoteDisplay from './components/QuoteDisplay.vue';

const selectedQuote = ref('');

const quotes = ref([
  'Если ты гей, то ты любишь мужчин',
  'Мужчины носят усы, усы носят мужчин',
  'Не всё то рыба, что плавает, может быть говно еще',
]);
</script>

<template>
  <section class="app">
    <h1 class="app__title">Генератор цитат</h1>

    <div class="top-section">
      <div class="quote-form">
        <QuoteForm v-model="quotes" />
      </div>

      <div class="random-quote">
        <QuoteDisplay v-model="quotes" />
      </div>
    </div>

    <div class="bottom-section">
      <QuoteList v-model="quotes" />
    </div>
  </section>
</template>

<style>
body {
  font-family: 'Roboto', sans-serif;
}

.app {
  max-width: 1200px;
  width: 100%;
  margin: 0 auto;
}
.app__title {
  font-size: 24px;
}

.top-section {
  display: flex;
  gap: 200px;
  justify-content: space-between;
  align-items: stretch;
  width: 100%;
}

.quote-form {
  min-width: 300px;
}

.random-quote {
  min-width: 300px;
  text-align: center;
}

.quote-list {
  width: 100%;
  margin-top: 20px;
}
</style>
