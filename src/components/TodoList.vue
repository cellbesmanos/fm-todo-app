<template>
  <TodoForm v-model="userInput" @add-task="addNewTask" />

  <TodoItemList @toggle-task="toggleTask" :tasks="sortedList" />
</template>

<script setup>
import { ref, computed } from "vue";
import TodoItemList from "./TodoItemList.vue";
import TodoForm from "./TodoForm.vue";

const userInput = ref("");
const sampleData = ref([
  {
    id: 1,
    task: "Write a cool JS library",
    isFinished: false,
  },
  {
    id: 2,
    task: "Make it generic enough",
    isFinished: false,
  },
  {
    id: 3,
    task: "Write README",
    isFinished: false,
  },
  {
    id: 4,
    task: "Create some examples",
    isFinished: false,
  },
  {
    id: 5,
    task: "Spam in Twitter and IRC to promote it",
    isFinished: false,
  },
  {
    id: 6,
    task: "???",
    isFinished: false,
  },
  {
    id: 7,
    task: "PROFIT",
    isFinished: false,
  },
]);
const itemsCount = computed(() => sampleData.value.length);
const sortedList = computed(() =>
  [...sampleData.value].sort((curr, prev) => curr.id < prev.id)
);

function addNewTask() {
  sampleData.value.push({
    id: itemsCount + 1,
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
