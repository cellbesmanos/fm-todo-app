<template>
  <div class="todoList__list flow">
    <ul class="flow">
      <p class="todoList__list-message" v-if="tasks.length < 1">
        Where is everyone?
      </p>
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

<style>
.todoList__list {
  margin-block-start: 1.6rem;
  margin-block-end: 3.2rem;
  border-radius: var(--bradius);
  background-color: var(--clr-blue-gray-300);
  box-sizing: var(--bshadow);
}

.todoList__list ul {
  transform: translateY(-1.2rem);
  height: 37rem;
  overflow-y: scroll;
  list-style-type: none;

  animation-name: showUp;
  animation-duration: 0.2s;
  animation-timing-function: ease-in-out;
  animation-fill-mode: forwards;
  opacity: 0;
}

@media screen and (min-width: 34.375em) {
  .todoList__list ul {
    height: 42rem;
  }
}

.todoList__list ul:first-child {
  border-top-left-radius: var(--bradius);
  border-top-right-radius: var(--bradius);
}

.todoList__list-message {
  font-size: 1.6rem;
  margin-block-start: 1.6rem;
  text-align: center;

  animation-name: showUp;
  animation-duration: 0.2s;
  animation-timing-function: ease-in-out;
  animation-fill-mode: forwards;
  opacity: 0;
}

@keyframes showUp {
  from {
    opacity: 0;
    transform: translateY(1.2rem);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
