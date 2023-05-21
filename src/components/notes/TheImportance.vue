<template>
  <ul>
    <li style="--clr: green" :class="{ active: modelValue === 'low' }">
      <button type="button" @click="activate('low')">low</button>
    </li>
    <li style="--clr: orange" :class="{ active: modelValue === 'medium' }">
      <button type="button" @click="activate('medium')">medium</button>
    </li>
    <li style="--clr: red" :class="{ active: modelValue === 'high' }">
      <button type="button" @click="activate('high')">high</button>
    </li>
  </ul>
</template>

<script setup>
const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

function activate(option) {
  emit('update:modelValue', option);
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  justify-content: center;
  gap: 1rem;
}

button {
  padding: 1rem 2rem;
  cursor: pointer;
  border: 0.1rem solid var(--clr);
  background-color: transparent;
}

button:hover {
  background-color: var(--clr);
  color: white;
}

.active button {
  background-color: var(--clr);
  color: white;
}
</style>