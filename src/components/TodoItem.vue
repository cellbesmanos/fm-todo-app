<template>
  <li class="todoItem" :class="{ 'todoItem--finished': isFinished }">
    <div class="todoItem__left">
      <button
        @click="handleClick($event)"
        type="button"
        role="checkbox"
        aria-label="mark as done"
        :aria-checked="isFinished"
        data-label="toggle"
        class="todoItem__toggle"
      >
        <svg
          v-if="isFinished"
          aria-hidden="true"
          xmlns="http://www.w3.org/2000/svg"
          width="10"
          height="10"
        >
          <path
            fill="none"
            stroke="#FFF"
            stroke-width="2"
            d="M1 4.304L3.696 7l6-6"
          />
        </svg>
      </button>
      <p>{{ task }}</p>
    </div>

    <button
      @click="handleClick($event)"
      type="button"
      aria-label="delete task"
      data-label="delete"
      class="todoItem__delete"
    >
      <svg
        width="12"
        height="12"
        viewBox="0 0 12 12"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M11.5194 0L12 0.479891L6.47992 6.00034L12 11.5201L11.5201 12L6 6.48023L0.479919 12L0 11.5187L5.52008 5.99898L0 0.479891L0.479919 0L6.00068 5.51977L11.5201 0H11.5194Z"
          fill="#494C6B"
        />
      </svg>
    </button>
  </li>
</template>

<script setup>
const { id, task, isFinished } = defineProps({
  id: Number,
  task: String,
  isFinished: Boolean,
});

const emit = defineEmits(["bubbleClick"]);

function handleClick(event) {
  emit("bubbleClick", { id, type: event.target.dataset.label });
}
</script>

<style>
.todoItem {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.2rem;
  min-height: 5.2rem;
  padding-inline: 2rem;
}

.todoItem__left {
  display: flex;
  align-items: center;
  gap: 1.2rem;
}

.todoItem__toggle {
  --size: 2rem;

  width: var(--size);
  height: var(--size);
  border-radius: 50%;
  border: 1px solid var(--clr-blue-gray-400);

  transition: border 0.2s ease-in, background-color 0.2s ease-in;
}

.todoItem__toggle:hover,
.todoItem__toggle:focus {
  border-width: 1px;
  border-color: var(--clr-blue);
}

.todoItem--finished .todoItem__toggle {
  background-image: linear-gradient(
    135deg,
    hsl(192, 100%, 67%),
    hsl(280, 87%, 65%)
  );
}

.todoItem__toggle svg {
  --size: 1rem;
  display: inline-block;
  width: var(--size);
  height: var(--size);
  margin-block-start: 0.5rem;

  transform: scaleX(0);

  animation-name: scaleUp;
  animation-duration: 0.1s;
  animation-timing-function: ease-in;
  animation-fill-mode: forwards;
  pointer-events: none;
}

.todoItem p {
  font-size: 1.2rem;
  letter-spacing: -0.01em;

  transition: text-decoration 0.2s ease-in, opacity 0.1s ease-in;
}

.todoItem--finished p {
  text-decoration: line-through;
  opacity: 0.5;
}

.todoItem__delete {
  transition: border-color 0.2s ease-in-out;
}

.todoItem__delete svg {
  margin-block-start: 0.5rem;
}

.todoItem__delete path {
  transition: fill 0.2s ease-in;
}

.todoItem__delete:hover path,
.todoItem__delete:focus path {
  fill: var(--clr-blue);
}
</style>
