<template>
  <div>
    <h2>
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

    mounted() {
      console.log(this.question);
    },
    methods: {},
  };
</script>
