<template>
  <div>
    <ul class="answers-box">
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
  .answers-box {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
  }
  .answer {
    width: 45%;
    list-style: none;
    border: 1px solid black;
    padding: 8px;
    margin-bottom: 1%;
    transition: 1s ease;
    border-radius: 2px;
    font-weight: bold;
  }

  .answer:hover {
    /* background-color: cornflowerblue; */
    cursor: pointer;
    transition: 1s ease;
  }

  .wrong {
    background-color: red;
  }

  .correct {
    background-color: green;
  }
</style>
