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
    background-color: #6158ac;
    -webkit-text-stroke-width: 0.5px;
    -webkit-text-stroke-color: rgb(31, 31, 31);
    color: white;
    margin: auto;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 80%;
    border: 1px solid rgb(88, 88, 88);
    border-radius: 50px;
  }
</style>
