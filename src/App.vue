<script setup lang="ts">
import { ref } from "vue";
import NotesCard from "./components/notes-card.vue"

const showModal = ref(false);
const newNoteText = ref("");

const getRandomColor = () => {
  const color = `hsl(${Math.random() * 360}, 100%, 75%)`;

  return color;
};

const errorMessage = ref("");
const notes = ref<any[]>([{
  id: Math.floor(Math.random() * 10000),
  description: 'adsasdadasd',
  backgroundColor: getRandomColor(),
}]);

const addNewNote = () => {
  if(newNoteText.value.length <= 10) {
    errorMessage.value = 'please enter message more than 10 characters';
    return;
  }

  errorMessage.value = '';

  notes.value.push({
    id: Math.floor(Math.random() * 10000),
    description: newNoteText.value,
    backgroundColor: getRandomColor(),
  });

  showModal.value = false;
  newNoteText.value = '';
};
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNoteText" name="textarea" cols="30" rows="10"></textarea>

        <span v-show="errorMessage" class="error-message">{{ errorMessage }}</span>

        <button
          class="add-note-btn"
          @click="addNewNote()"
        >
          Add Note
        </button>
        <button @click="showModal = false" class="close-note-btn">close</button>
      </div>
    </div>
    
    <div class="container">
      <header>
        <h1>Notes</h1>

        <button @click="showModal = true">+</button>
      </header>

      <div class="cards-container">
        <NotesCard
          v-for="note in notes"
          :key="note.id"
          :style="{'background-color': note.backgroundColor}"
        >
          <p class="main-text">{{ note.description }}</p>
        </NotesCard>
      </div>
    </div>
  </main>
</template>

<style scoped>
.container {
  max-width: 1000px;
  margin: 0 auto;
  padding: 0;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}

.container button {
  width: 50px;
  height: 50px;
  border: none;
  background-color: black;
  color: white;
  border-radius: 100%;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
}

.date {
  font-size: 12px;
  font-weight: bold;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.77);
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.modal button {
  padding: 10px 20px;
  width: 100%;
  font-size: 20px;
  background: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
}

.modal .close-note-btn {
  background-color: red;
}

.modal .error-message {
  color: red;
}
</style>
