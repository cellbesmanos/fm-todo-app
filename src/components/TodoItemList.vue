<template>
  <div>
    <TodoItem v-for="{ id, task } in tasks" :key="id" :task="task" />
  </div>
</template>

<script setup>
import TodoItem from "./TodoItem.vue";

const { tasks } = defineProps({
  tasks: Array,
});
</script>
