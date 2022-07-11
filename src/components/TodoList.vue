<template>
  <TodoForm v-model="userInput" @add-task="addNewTask" />

  <TodoItemList @toggle-task="toggleTask" :tasks="sampleData">
    <TodoListToolbar :remainingTasks="remainingTasks" />
  </TodoItemList>
</template>

<script setup>
import { ref, computed } from "vue";
import TodoItemList from "./TodoItemList.vue";
import TodoForm from "./TodoForm.vue";
import TodoListToolbar from "./TodoListToolbar.vue";

const userInput = ref("");
const sampleData = ref([
  {
    id: 0,
    task: "Write a cool JS library",
    isFinished: false,
  },
  {
    id: 1,
    task: "Make it generic enough",
    isFinished: false,
  },
  {
    id: 2,
    task: "Write README",
    isFinished: false,
  },
  {
    id: 3,
    task: "Create some examples",
    isFinished: false,
  },
  {
    id: 4,
    task: "Spam in Twitter and IRC to promote it",
    isFinished: false,
  },
  {
    id: 5,
    task: "???",
    isFinished: false,
  },
  {
    id: 6,
    task: "PROFIT",
    isFinished: false,
  },
]);
const itemIdCount = ref(sampleData.value.length);
const remainingTasks = computed(
  () => sampleData.value.filter((task) => task.isFinished === false).length
);

function addNewTask() {
  sampleData.value.push({
    id: itemIdCount.value++,
    task: userInput.value,
  });
  userInput.value = "";
}

function toggleTask(id) {
  const [item] = sampleData.value.filter((item) => item.id == id);
  const remaining = sampleData.value.filter((item) => item.id !== id);
  sampleData.value = [{ ...item, isFinished: !item.isFinished }, ...remaining];
}
</script>
