<template>
  <div>
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

    <slot>Missing Toolbar Component</slot>
  </div>
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
