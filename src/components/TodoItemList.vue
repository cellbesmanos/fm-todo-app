<template>
  <ul>
    <TodoItem v-for="{ id, task } in tasks" :key="id" :task="task" />
  </ul>
</template>

<script setup>
import TodoItem from "./TodoItem.vue";

const { tasks } = defineProps({
  tasks: Array,
});
</script>
