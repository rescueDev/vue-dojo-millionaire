<template>
  <div id="app">
    <img alt="Millionaire logo" src="./assets/logo.png" />
    <div>
      <button @click="startGame">Start Game</button>
    </div>
    <Container
      :question="quest.question"
      :answers="quest.answers"
      :correct="quest.correct"
      @check-answer="checkAnswer"
    >
    </Container>
  </div>
</template>

<script>
  import Container from "@/components/Container.vue";
  import questions from "@/questions";

  export default {
    name: "App",
    components: {
      Container,
    },

    data() {
      return {
        questions: questions,
        quest: {
          question: "",
          answers: [],
        },
        block: 0,
        points: 0,
      };
    },

    methods: {
      startGame() {
        this.randomQuestion();
      },
      randomQuestion() {
        //disable button
        //get first block questions
        var firstQuestion = this.questions[this.block].questions;

        //get random question from first block
        let random =
          firstQuestion[Math.floor(Math.random() * firstQuestion.length)];

        //assign question, answers and correct
        this.quest = {
          question: random.question,
          answers: random.content,
          correct: random.correct,
        };
      },

      checkAnswer(index, answer, results) {
        console.log("app.vue emit dati", answer, index, results);
        if (this.quest.correct === index) {
          this.points++;
          console.log("bravo, giusta", this.points);
        }

        this.next = results;

        //filter questions
        var asked = this.questions[this.block].questions.find(
          (el) => el.question === this.quest.question
        );

        //target question id
        const ind = this.questions[this.block].questions.indexOf(asked);

        //remove question in array questions
        if (ind > -1) {
          this.questions[this.block].questions.splice(ind, 1);
        }

        //pass to second and more block of questions (much difficult)
        if (this.questions[this.block].questions.length === 0) {
          this.block++;
        }
      },
    },
  };
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
