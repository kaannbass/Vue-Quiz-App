<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
    <questions
      :questions="questions"
      :questionsAnsweered="questionsAnsweered"
      v-if="questionsAnsweered < questions.length"
      @question-answered="questionanswered"
    />
    <result v-else :results="results" :totalCorrect="totalCorrect" />
    </transition>
    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="this.questionsAnsweered === questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script>
import questions from "./components/Questions.vue";
import result from "./components/Result.vue";
export default {
  name: "App",
  components: {
    questions,
    result,
  },
  data: () => ({
    totalCorrect: 0,
    questionsAnsweered: 0,
    questions: [
      {
        q: "What is 2 + 2?",
        answers: [
          {
            text: "4",
            is_correct: true,
          },
          {
            text: "3",
            is_correct: false,
          },
          {
            text: "Fish",
            is_correct: false,
          },
          {
            text: "5",
            is_correct: false,
          },
        ],
      },
      {
        q: 'How many letters are in the word "Banana"?',
        answers: [
          {
            text: "5",
            is_correct: false,
          },
          {
            text: "7",
            is_correct: false,
          },
          {
            text: "6",
            is_correct: true,
          },
          {
            text: "12",
            is_correct: false,
          },
        ],
      },
      {
        q: "Find the missing letter: C_ke",
        answers: [
          {
            text: "e",
            is_correct: false,
          },
          {
            text: "a",
            is_correct: true,
          },
          {
            text: "i",
            is_correct: false,
          },
        ],
      },
    ],
    results: [
      {
        min: 0,
        max: 2,
        title: "Try again!",
        desc: "Do a little more studying and you may succeed!",
      },
      {
        min: 3,
        max: 3,
        title: "Wow, you're a genius!",
        desc: "Studying has definitely paid off for you!",
      },
    ],
  }),
  methods: {
    questionanswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
      }
      this.questionsAnsweered++;
    },
    reset() {
      this.questionsAnsweered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
