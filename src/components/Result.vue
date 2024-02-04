<template>
  <div class="results">
    <p>Your Results...</p>
    <h1>{{ total }}/{{ quizLength }}</h1>
    <RouterLink :to="{ name: 'home' }">Go Back</RouterLink>
  </div>
</template>

<script setup>
defineProps({
  total: {
    type: Number,
    required: true,
  },
  quizLength: {
    type: Number,
    requored: true,
  },
});
</script>

<style scoped>
.results {
  text-align: center;
  padding: 100px 0;
}

p {
  font-size: 25px;
}

h1 {
  font-size: 80px;
}
</style>