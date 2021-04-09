<template>
  <div>
    <question :question="question" />
    <answer :answers="answers" :correct="correct" @check-answer="checkAnswer" />
  </div>
</template>

<script>
  import Question from "@/components/Question.vue";
  import Answer from "@/components/Answer.vue";
  export default {
    components: {
      Answer,
      Question,
    },
    props: {
      question: String,
      answers: Array,
      correct: Number,
    },
    methods: {
      checkAnswer(answer, index, results) {
        console.log("container emits", index, answer);
        this.$emit("check-answer", index, answer, results);
      },
    },
  };
</script>
