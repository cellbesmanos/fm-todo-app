<template>
  <form @submit.prevent="addNewTask">
    <input
      v-model.trim="userInput"
      type="text"
      placeholder="Feed the dogs..."
    />

    <button type="submit">Add Task</button>
  </form>

  <TodoItemList :tasks="reversedList" />
</template>

<script setup>
import { ref, computed } from "vue";
import TodoItemList from "./TodoItemList.vue";

const userInput = ref("");
const sampleData = ref([
  {
    id: 1,
    task: "Write a cool JS library",
  },
  {
    id: 2,
    task: "Make it generic enough",
  },
  {
    id: 3,
    task: "Write README",
  },
  {
    id: 4,
    task: "Create some examples",
  },
  {
    id: 5,
    task: "Spam in Twitter and IRC to promote it",
  },
  {
    id: 6,
    task: "???",
  },
  {
    id: 7,
    task: "PROFIT",
  },
]);
const itemsCount = computed(() => sampleData.value.length);
const reversedList = computed(() => [...sampleData.value].reverse());

function addNewTask() {
  sampleData.value.push({
    id: itemsCount + 1,
    task: userInput.value,
  });
  userInput.value = "";
}
</script>
