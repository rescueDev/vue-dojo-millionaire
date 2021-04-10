<template>
  <div v-if="question">
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
      // console.log(this.question);
    },
    methods: {},
  };
</script>

<style scoped>
  div {
    margin: auto;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 80%;
    border: 1px solid black;
    border-radius: 50px;
  }
</style>
