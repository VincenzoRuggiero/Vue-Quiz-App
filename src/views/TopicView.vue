<template>
  {{ barPercentage }}
  <div>
    <QuizHeader
      :questionStatus="questionStatus"
      :barPercentage="barPercentage" />
    <div>
      <QuestionComp
        :question="quiz.questions[currentQuestionIndex]"
        @selectOption="onOptionSelected" />
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
const numberOfCorrectAnswers = ref(0);

const onOptionSelected = (isCorrect) => {
  if (isCorrect) {
    numberOfCorrectAnswers.value++;
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
