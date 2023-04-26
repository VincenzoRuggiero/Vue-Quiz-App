<template>
  {{ barPercentage }}
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
import { useRoute } from "vue-router";
import { computed } from "@vue/reactivity";
import { ref } from "vue";
import quizes from "../data/quizes.json";

const route = useRoute();
const quizId = parseInt(route.params.id);
const quiz = quizes.find((q) => q.id === quizId);
const currentQuestionIndex = ref(0);

const questionStatus = computed(
  () => `${currentQuestionIndex.value}/${quiz.questions.length}`
);

const barPercentage = computed(
  () => `${(currentQuestionIndex.value / quiz.questions.length) * 100}%`
);
</script>

<style scoped></style>
