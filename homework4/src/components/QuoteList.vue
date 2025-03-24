<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
  modelValue: {
    type: Array,
    default: () => [],
  },
});
const emit = defineEmits(['update:modelValue', 'select-quote']);

const quotes = ref([...props.modelValue]);

watch(
  () => props.modelValue,
  (newVal) => {
    quotes.value = [...newVal];
  }
);

const removeQuote = (index) => {
  quotes.value.splice(index, 1);
  emit('update:modelValue', quotes.value);
};

const copyQuote = (quote, event) => {
  navigator.clipboard.writeText(quote);
  const button = event.target;
  button.textContent = 'Скопировано!';
  setTimeout(() => {
    button.textContent = 'Копировать';
  }, 1500);
};
</script>

<template>
  <div class="quote-list">
    <TransitionGroup name="fade" tag="ul" class="quote-list-inner">
      <li
        v-for="(quote, index) in quotes"
        :key="`${quote}-${index}`"
        class="quote-list__item"
      >
        <span class="quote-list__item-text"> "{{ quote }}" </span>
        <div class="quote-list__item-actions">
          <button @click="removeQuote(index)">Удалить</button>
          <button @click="copyQuote(quote, $event)">Копировать</button>
        </div>
      </li>
    </TransitionGroup>
  </div>
</template>

<style scoped>
.quote-list-inner {
  list-style: none;
  padding: 0;
}
.quote-list__item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5em;
  border-bottom: 1px solid #ccc;
  transition: ease 0.3s;
}
.quote-list__item-text {
  display: block;
  max-width: 500px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  transition: ease 0.3s;
}

.quote-list__item-text:hover {
  opacity: 0.5;
  cursor: pointer;
}
.quote-list__item-actions {
  display: flex;
  gap: 10px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease, transform 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
