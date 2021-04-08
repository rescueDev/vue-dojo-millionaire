<template>
  <div>
    <question :question="question" />
    <answer :answers="answers" />
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
    },
  };
</script>
