<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width:`${(questionsAnsweered/questions.length)*100}%`}"
      ></div>
      <div class="status">
        {{ questionsAnsweered }} out of {{ questions.length }} questions
        answered
      </div>
    </div>
    <transition-group name="fade">
    <div
      class="single-question"
      v-for="(question, qi) in questions"
      :key="question.q"
      v-show="questionsAnsweered === qi"
    >
      <div class="question">{{ question.q }}</div>
      <div class="answers">
        <div
          class="answer"
          v-for="answers in question.answers"
          :key="answers.text"
          @click.prevent="selectAnswer(answers.is_correct)"
        >
          {{ answers.text }}
        </div>
      </div>
    </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: ["questions", "questionsAnsweered"],
  emits: ["question-answered"],
  methods: {
    selectAnswer(is_correct) {
      this.$emit("question-answered", is_correct);
    },
  },
};
</script>
