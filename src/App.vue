<template>
  <div class="container">
    <header>
      <h1>Quizes</h1>
      <input v-model.trim="search" type="text" placeholder="Search..." />
    </header>
    <div class="options-container">
      <CardComp v-for="quiz in quizes" :key="quiz.id" :quiz="quiz" />
      <!-- <div v-for="quiz in quizzes" :key="quiz.id" class="card">
        <img :src="quiz.img" :alt="`${quiz.name} Questions`" />
        <div class="card-text">
          <h2>{{ quiz.name }}</h2>
          <p>{{ quiz.questions.length }} Questions</p>
        </div>
      </div> -->
    </div>
  </div>
</template>

<script setup>
import q from "./data/quizzes.json";
import { ref, watch } from "vue";

import CardComp from "./components/CardComp.vue";

const quizes = ref(q);
const search = ref("");

// Watch enables update of content displayed when searched
watch(search, () => {
  // Quizzes value is equal to the name value searched
  quizzes.value = q.filter((quiz) =>
    quiz.name.toLowerCase().includes(search.value.toLowerCase())
  );
});
</script>

<style scoped>
.container {
  max-width: 1000px;
  margin: 0 auto;
}

header {
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
}

header h1 {
  font-weight: bold;
  margin-right: 30px;
}

header input {
  border: none;
  background-color: rgba(128, 128, 128, 0.1);
  padding: 10px;
  border-radius: 5px;
}

.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}

/* Card Styling */
</style>
