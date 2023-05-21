<template>
  <li>
    <base-card :class="importance">
      <header>
        <h3>{{ title }}</h3>
        <base-button mode="flat" @click="removeNote(id)">Delete</base-button>
      </header>
      <p>{{ description }}</p>
      <i>{{ date }}</i>
    </base-card>
  </li>
</template>

<script setup>
import { inject } from "vue";

const props = defineProps(['id', 'title', 'description', 'date', 'importance']);
const removeNote = inject("removeNote");
</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

i {
  text-decoration: none;
}
</style>