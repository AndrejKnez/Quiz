  <template>
  <div>
    <header>
      <h1>Quizes</h1>
      <input
        type="text"
        placeholder="Search..."
        v-model="searchQuiz"
        @input="searchQuizes"
      />
    </header>
    <div class="options-container">
      <Card
        v-for="quiz in quizes"
        :key="quiz.id"
        :quiz="quiz"
        @click="navigateToQuiz(quiz.id)"
      />
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from "vue";
import data from "../data/quizes.json";
import Card from "../components/Card.vue";
import { useRouter } from "vue-router";

const router = useRouter();

const quizes = ref(data);

const searchQuiz = ref(null);

const searchQuizes = computed(() => {
  if (searchQuiz.value != "") {
    quizes.value = quizes.value.filter((el) =>
      el.name.toLowerCase().includes(searchQuiz.value.toLowerCase())
    );
  } else {
    quizes.value = data;
  }
});

const navigateToQuiz = (id) => {
  router.push({
    name: "QuizView",
    params: {
      id: id,
    },
  });
};
</script>

<style scoped>
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

/* CARD */
</style>