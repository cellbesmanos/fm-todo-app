<template>
  <div>
    <ul>
      <p v-if="tasks.length < 1">There is nothing in here.</p>
      <TodoItem
        v-else
        v-for="{ id, task, isFinished } in tasks"
        @bubble-click="handleClick"
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

const emit = defineEmits(["toggleTask", "deleteTask"]);

function handleClick({ id, type }) {
  switch (type) {
    case "toggle":
      emit("toggleTask", id);
      break;
    case "delete":
      emit("deleteTask", id);
      break;
    default:
      throw new Error("Invalid click type from task item");
  }
}
</script>
