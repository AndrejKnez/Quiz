<template>
  <div class="question-container">
    <h1 class="question">
      {{ question.text }}
    </h1>
  </div>
  <div class="options-container">
    <div v-for="option in question.options" :key="option.id" class="option">
      <p class="option-label">{{ option.label }}</p>
      <div class="option-value" @click="questionAnswered(option.isCorrect)">
        <p>{{ option.text }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const totalPoints = ref(0);

const currentQuestion = ref(0);
defineProps({
  question: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["question-answered"]);

const questionAnswered = (correct) => {
  if (correct) {
    totalPoints.value++;
  }
  emit("question-answered", totalPoints.value);
};
</script>

<style scoped>
.question-container {
  margin-top: 20px;
}

.question {
  font-size: 40px;
  margin-bottom: 20px;
}

.option {
  display: flex;
  margin-bottom: 20px;
  cursor: pointer;
}

.option-label {
  background-color: bisque;
  width: 50px;
  height: 50px;
  font-size: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.option-value {
  background-color: rgb(244, 239, 239);
  width: 100%;
  font-size: 30px;
  padding: 0 20px;
}
</style>