<template>
  <div class="results">
    <p>Your results...</p>
    <h1>{{ numberOfCorrectAnswers }}/{{ quizQuestionLength }}</h1>
    <router-link to="/">Go back</router-link>
  </div>
</template>

<script setup>
import { defineProps } from "vue";
import { RouterLink } from "vue-router";

const { numberOfCorrectAnswers, quizQuestionLength } = defineProps([
  "quizQuestionLength",
  "numberOfCorrectAnswers",
]);
</script>

<style scoped>
.results {
  text-align: center;
  padding: 100px 0px;
}

p {
  font-size: 25px;
}

h1 {
  font-size: 80px;
}
</style>
