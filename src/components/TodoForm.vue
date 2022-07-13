<template>
  <form @submit.prevent="$emit('addTask')" class="todoList__form">
    <button
      class="todoList__form-submit"
      type="submit"
      aria-label="add task"
      :disabled="submitDisabled"
    >
      <svg
        width="10"
        height="10"
        viewBox="0 0 10 10"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M5 1V9M9 5H1"
          stroke="white"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
    </button>

    <input
      :value="modelValue"
      @input="handleInput($event)"
      type="text"
      placeholder="Feed the dogs..."
    />
  </form>
</template>

<script setup>
defineProps(["modelValue", "submitDisabled"]);
const emit = defineEmits(["update:modelValue", "addTask"]);

function toProperCase(str) {
  if (!str) {
    return;
  }
  return `${str[0].toUpperCase()}${str.slice(1)}`;
}

function handleInput(event) {
  emit("update:modelValue", toProperCase(event.target.value));
}
</script>

<style>
.todoList__form {
  display: flex;
  align-items: center;
  gap: 1.2rem;
  min-height: 4.8rem;
  padding-inline: 2rem;
  background-color: white;
  border-radius: var(--bradius);
  box-shadow: var(--bshadow);
}

.todoList__form-submit {
  --size: 2rem;

  display: flex;
  align-items: center;
  justify-content: center;
  width: var(--size);
  height: var(--size);
  border-radius: 50%;
  border: 1px solid var(--clr-blue-gray-400);

  transition: border 0.2s ease-in, background-color 0.2s ease-in;
}

.todoList__form-submit:disabled {
  pointer-events: none;
}

.todoList__form-submit:disabled svg {
  display: none;
}

.todoList__form-submit:enabled {
  background-image: linear-gradient(
    135deg,
    hsl(192, 100%, 67%),
    hsl(280, 87%, 65%)
  );
}

.todoList__form-submit:enabled:hover,
.todoList__form-submit:enabled:focus {
  border-width: 1px;
  border-color: var(--clr-blue);
}

.todoList__form-submit:enabled svg {
  display: block;
  transform: scaleX(0);

  animation-name: scaleUp;
  animation-duration: 0.1s;
  animation-timing-function: ease-in;
  animation-fill-mode: forwards;
  pointer-events: none;
}

.todoList__form input {
  flex-grow: 2;
  border: none;
}
</style>
