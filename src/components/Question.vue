<template>
  <div>
    <h2>
      Question:
      {{ question }}
    </h2>
  </div>
</template>

<script>
  // import questions from "@/questions.js";
  export default {
    props: {
      question: String,
    },
    // inject: { question: "question" },
    mounted() {
      console.log(this.question);
    },
    methods: {},
  };
</script>
