<template>
  <div>
    <TodoItemList :tasks="sampleData" />
  </div>
</template>

<script setup>
import TodoItemList from "./TodoItemList.vue";

const sampleData = [
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
];
</script>
