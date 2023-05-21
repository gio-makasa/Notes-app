<template>
  <base-dialog v-if="invalidInput" title="Invalid Input" @close="confirmError">
    <template #default>
      <p>Input value is invalid</p>
      <p>All input must have at least 1 charachter</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>

  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">title</label>
        <input type="text" id="title" name="title" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">description</label>
        <textarea name="description" id="description" cols="3" ref="descInput"></textarea>
      </div>
      <div class="form-control">
        <label>importance</label>
        <TheImportance v-model="importance" />
      </div>
      <div class="form-control">
        <label for="date">date</label>
        <input type="date" id="date" name="date" ref="dateInput" />
      </div>
      <div>
        <base-button type="submit">Add Note</base-button>
      </div>
    </form>
  </base-card>
</template>

<script setup>
import { ref, inject } from 'vue';
import TheImportance from "./TheImportance.vue";

const addNote = inject("addNote");
const invalidInput = ref(false);
const importance = ref(null);
const titleInput = ref(null);
const descInput = ref(null);
const dateInput = ref(null);

function submitData() {
  let enteredTitle = titleInput.value.value;
  let enteredDesc = descInput.value.value;
  let enteredDate = dateInput.value.value;
  let enteredImportance = importance.value || "low";
  if (
    enteredTitle.trim() == "" ||
    enteredDesc.trim() == "" ||
    enteredDate.trim() == ""
  ) {
    invalidInput.value = true;
    return;
  }

  addNote(enteredTitle, enteredDesc, enteredDate, enteredImportance);

  titleInput.value.value = "";
  descInput.value.value = "";
  dateInput.value.value = "";
  importance.value = null;
}

function confirmError() {
  invalidInput.value = false;
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
  text-transform: capitalize;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>