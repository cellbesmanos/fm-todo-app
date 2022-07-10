<template>
  <ul>
    <TodoItem
      @bubble-click="handleClick"
      v-for="{ id, task, isFinished } in tasks"
      :key="id"
      :id="id"
      :task="task"
      :is-finished="isFinished"
    />
  </ul>
</template>

<script setup>
import TodoItem from "./TodoItem.vue";

const { tasks } = defineProps({
  tasks: Array,
});

const emit = defineEmits(["toggleTask"]);

function handleClick(id) {
  emit("toggleTask", id);
}
</script>
