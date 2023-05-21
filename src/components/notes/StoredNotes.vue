<template>
  <ul v-if="storedNotes.length > 0">
    <NoteItem
      v-for="note in storedNotes"
      :key="note.id"
      :id="note.id"
      :title="note.title"
      :description="note.description"
      :date="note.date"
      :importance="note.importance"
    />
  </ul>
  <div v-else class="noNotes">
    <p>there are no notes.</p>
  </div>
</template>

<script setup>
import { inject } from 'vue';
import NoteItem from './NoteItem.vue';

const storedNotes = inject("storedNotes");
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}

.noNotes {
  text-align: center;
  font-size: larger;
}
</style>