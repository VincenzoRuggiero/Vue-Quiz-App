<template>
  <div>
    <QuizHeader
      :questionStatus="questionStatus"
      :barPercentage="barPercentage" />
    <div>
      <QuestionComp :question="quiz.questions[currentQuestionIndex]" />
    </div>
  </div>
</template>

<script setup>
import QuestionComp from "../components/QuestionComp.vue";
import QuizHeader from "../components/QuizHeader.vue";
import { useRoute, watch, computed } from "vue-router";
import { ref } from "vue";
import quizes from "../data/quizes.json";

const route = useRoute();

const quizId = parseInt(route.params.id);

const quiz = quizes.find((q) => q.id === quizId);

const currentQuestionIndex = ref(0);

// const questionStatus = `${currentQuestionIndex.value}/${quiz.questions.length}`;

// watch(
//   () => currentQuestionIndex.value,
//   () => {
//     questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`;
//   }
// );

const questionStatus = computed(() => {
  return `${currentQuestionIndex.value}/${quiz.questions.length}`;
});

const barPercentage = computed(
  () => `${(currentQuestionIndex.value / quiz.questions.length) * 100}%`
);
</script>

<style scoped></style>
