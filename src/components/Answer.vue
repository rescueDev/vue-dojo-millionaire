<template>
  <div>
    <ul class="mt-4 answers-box">
      <li
        :class="[
          light === true && index === selected
            ? 'light answer'
            : results === true
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
  export default {
    data() {
      return {
        selected: null,
        light: false,
        id: null,
        answer: "",
        results: false,
        points: 0,
        confirm: false,
      };
    },
    props: {
      answers: Array,
      correct: Number,
    },
    methods: {
      checkAnswer(answer, index) {
        this.light = true;
        console.log("Light", this.light);
        this.selected = index;
        console.log("Index", this.selected);
        this.answer = answer;

        setTimeout(() => {
          var result = window.confirm("Are you sure?");
          if (result === true) {
            // this.light = false;
            this.confirm = true;

            this.id = index;
            this.selected = index;
            this.answer = answer;
            // this.light = false;

            setTimeout(() => {
              this.light = false;
              this.results = true;
              this.$emit("check-answer", this.answer, this.id, this.results);
            }, 3000);
          } else {
            console.log("pressed cancel");
            this.light = false;
            this.confirm = false;
            this.id = "";
            this.answer = "";
            this.results = false;
            this.light = false;
          }
        }, 2000);
      },
      clear() {
        this.light = false;
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
    background-color: #6158ac;
    -webkit-text-stroke-width: 0.5px;
    -webkit-text-stroke-color: rgb(31, 31, 31);
    list-style: none;
    border: 1px solid rgb(88, 88, 88);
    padding: 8px;
    margin-bottom: 1%;
    transition: 1s ease;
    border-radius: 50px;
    font-weight: bold;
    color: white;
  }

  .answer:hover {
    cursor: pointer;
    transition: 1s ease;
  }

  .wrong {
    background-color: rgba(231, 20, 20, 0.9);
    color: white;
  }

  .correct {
    background-color: rgba(17, 146, 17, 0.9);
    color: white;
    animation: blinkingCorrect 2s infinite;
  }

  @keyframes blinkingCorrect {
    0% {
      background-color: rgba(17, 146, 17, 0.9);
    }
    25% {
      background-color: #6158ac;
    }
    50% {
      background-color: rgba(17, 146, 17, 0.9);
    }
    75% {
      background-color: #6158ac;
    }
    100% {
      background-color: rgba(17, 146, 17, 0.9);
    }
  }

  .light {
    background-color: rgba(255, 145, 0, 0.9);
    color: white;
    animation: blinkingSelected 2s infinite;
  }
  @keyframes blinkingSelected {
    0% {
      background-color: rgba(255, 145, 0, 0.9);
    }
    25% {
      background-color: #6158ac;
    }
    50% {
      background-color: rgba(255, 145, 0, 0.9);
    }
    75% {
      background-color: #6158ac;
    }
    100% {
      background-color: rgba(255, 145, 0, 0.9);
    }
  }
</style>
