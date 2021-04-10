<template>
  <div>
    <ul class="mt-4 answers-box">
      <li
        :class="[
          results === true
            ? index === correct
              ? 'correct answer'
              : 'wrong answer'
            : 'answer',
        ]"
        v-for="(answer, index) in answers"
        :key="index"
        @click="checkAnswer(answer, index)"
      >
        {{ answer }}
      </li>
    </ul>
  </div>
</template>

<script>
  // import questions from "@/questions";
  export default {
    data() {
      return {
        id: null,
        answer: "",
        results: false,
        points: 0,
      };
    },
    props: {
      answers: Array,
      correct: Number,
    },
    methods: {
      checkAnswer(answer, index) {
        this.results = true;
        this.id = index;
        this.answer = answer;
        this.$emit("check-answer", this.answer, this.id, this.results);
      },
      clear() {
        this.results = false;
      },
    },
  };
</script>

<style scoped>
  div {
    display: flex;
    width: 80%;
    margin: auto;
  }

  .answers-box {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: center;
  }
  .answer {
    width: 40%;
    list-style: none;
    border: 1px solid rgb(88, 88, 88);
    padding: 8px;
    margin-bottom: 1%;
    transition: 1s ease;
    border-radius: 50px;
  }

  .answer:hover {
    cursor: pointer;
    transition: 1s ease;
  }

  .wrong {
    background-color: rgba(246, 82, 82, 0.835);
  }

  .correct {
    background-color: rgba(81, 233, 81, 0.438);
  }
</style>
