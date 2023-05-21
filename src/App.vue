<template>
  <TheHeader header="Notes" />
  <TheNotes />
</template>

<script setup>
import TheHeader from './components/layout/TheHeader.vue';
import TheNotes from './components/notes/TheNotes.vue';
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Roboto', sans-serif;
}

body {
  margin: 0;
}
</style>