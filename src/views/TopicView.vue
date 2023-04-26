<template>
  {{ barPercentage }}
  <div>
    <QuizHeader
      :questionStatus="questionStatus"
      :barPercentage="barPercentage" />
    <div>
      <QuestionComp
        v-if="!showResults"
        :question="quiz.questions[currentQuestionIndex]"
        @selectOption="onOptionSelected" />
      <ResultComp
        v-else
        :quizQuestionLength="quiz.questions.length"
        :numberOfCorrectAnswers="numberOfCorrectAnswers" />
    </div>
  </div>
</template>

<script setup>
import QuestionComp from "../components/QuestionComp.vue";
import QuizHeader from "../components/QuizHeader.vue";
import ResultComp from "../components/ResultComp.vue";
import { useRoute } from "vue-router";
import { computed } from "@vue/reactivity";
import { ref } from "vue";
import quizes from "../data/quizes.json";

const route = useRoute();
const quizId = parseInt(route.params.id);
const quiz = quizes.find((q) => q.id === quizId);
const currentQuestionIndex = ref(0);
const numberOfCorrectAnswers = ref(0);
const showResults = ref(false);

const onOptionSelected = (isCorrect) => {
  if (isCorrect) {
    numberOfCorrectAnswers.value++;
  }

  if (quiz.questions.length - 1 === currentQuestionIndex.value) {
    showResults.value = true;
  }

  currentQuestionIndex.value++;
};
const questionStatus = computed(
  () => `${currentQuestionIndex.value}/${quiz.questions.length}`
);
const barPercentage = computed(
  () => `${(currentQuestionIndex.value / quiz.questions.length) * 100}%`
);
</script>

<style scoped></style>
