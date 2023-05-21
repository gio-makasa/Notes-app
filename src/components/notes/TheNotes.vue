<template>
  <base-card>
    <base-button @click="setSelectedTab('stored-notes')" :mode="storedButtonMode">Stored Notes</base-button>
    <base-button @click="setSelectedTab('add-notes')" :mode="addButtonMode">Add Note</base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab == 'stored-notes'? storedNotes: addNotes"></component>
  </keep-alive>
</template>

<script setup>
import { ref, computed, provide } from 'vue';
import storedNotes from './StoredNotes.vue';
import addNotes from './AddNotes.vue';

const selectedTab = ref('stored-notes')
const storedNotesArr = ref([])

provide('storedNotes', storedNotesArr)
provide('addNote', addNote)
provide('removeNote', removeNote)

const storedButtonMode = computed(function () {
  return selectedTab.value == 'stored-notes' ? null : 'flat';
})
const addButtonMode = computed(function () {
  return selectedTab.value == 'add-notes' ? null : 'flat';
})

function setSelectedTab(tab) {
  selectedTab.value = tab;
}

function addNote(title, desc, date, importance) {
  let newNote = {
    id: new Date().toISOString,
    title: title,
    description: desc,
    date: date,
    importance: importance,
  };

  storedNotesArr.value.unshift(newNote);
  selectedTab.value = 'stored-notes';
  sortNotes();
}

function removeNote(noteId) {
  let idx = storedNotesArr.value.findIndex((note) => note.id == noteId);
  storedNotesArr.value.splice(idx, 1);
  sortNotes();
}

function sortNotes() {
  storedNotesArr.value.sort(function (a, b) {
    if (a.importance == 'high') return -1;
    if (a.importance == 'low') return 1;
    if (a.importance == 'medium' && b.importance == 'high') return 1;
    if (a.importance == 'medium' && b.importance == 'low') return -1;
  });
  storedNotesArr.value.sort(function (a, b) {
    return a.date - b.date;
  });
  localStorage.setItem('Notes', JSON.stringify(storedNotesArr.value));
}

if (localStorage.Notes) {
  JSON.parse(localStorage.getItem('Notes')).forEach((note) => {
    storedNotesArr.value.push(note);
  });
}
</script>