<template>
  <QuizHeader :questionStatus="questionStatus" :barPercentage="barPercentage" />
  <Question
    :question="quiz.questions[currentQuestion]"
    @question-answered="questionAnswered"
    v-if="!endQuiz"
  />
  <Result v-else :total="totalPoints" :quizLength="quiz.questions.length" />
</template>

<script setup>
import data from "../data/quizes.json";
import { useRoute } from "vue-router";
import { computed, ref } from "vue";
import QuizHeader from "@/components/QuizHeader.vue";
import Question from "@/components/Question.vue";
import Result from "@/components/Result.vue";

const route = useRoute();
const quizId = parseInt(route.params.id);
const currentQuestion = ref(0);
const endQuiz = ref(false);
const totalPoints = ref(0);

const quiz = data.find((el) => el.id === quizId);

const questionStatus = computed(
  () => `${currentQuestion.value}/${quiz.questions.length}`
);
const barPercentage = computed(
  () => `${(currentQuestion.value / quiz.questions.length) * 100}%`
);

const questionAnswered = (total) => {
  currentQuestion.value++;
  if (currentQuestion.value === quiz.questions.length) {
    totalPoints.value = total;
    endQuiz.value = true;
  }
};
</script>

<style>
</style> 