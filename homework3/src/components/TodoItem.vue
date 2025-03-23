<script setup>
import { ref } from 'vue';
defineProps(['task', 'theme']);
defineEmits(['toggleTaskCompletion', 'removeTask']);
</script>

<template>
  <li
    class="todo__list_item"
    :class="[{ completed: task.completed }, `todo__item_theme-${theme}`]"
  >
    <div class="todo__task_info">
      <span class="todo__task_id">{{ task.id }}.</span>
      <span class="todo__task_name">{{ task.name }}</span>
      <span class="todo__task_created">({{ task.createdAt }})</span>
      <p class="todo__task_desc">{{ task.description }}</p>
    </div>
    <div class="todo__task_actions">
      <button @click="$emit('toggleTaskCompletion', task.id)">
        {{ task.completed ? 'Отменить' : 'Выполнено' }}
      </button>
      <button @click="$emit('removeTask', task.id)">Удалить</button>
    </div>
  </li>
</template>

<style scoped>
.todo__list_item.dark {
  background-color: darkgrey !important;
}

.todo__item_theme-default {
  background-color: darkgrey !important;
}

.todo__item_theme-dark {
  background-color: blue !important;
}

.todo__item_theme-cringe {
  background-color: yellow !important;
}

.todo__list_item.completed {
  text-decoration: line-through;
  color: gray;
}
</style>
