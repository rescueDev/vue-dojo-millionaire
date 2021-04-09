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
        // this.question = random.question;
        // this.answers = random.content;

        this.quest = {
          question: random.question,
          answers: random.content,
          correct: random.correct,
        };

        this.questions;
        // console.log(this.quest);
      },
      checkAnswer(index, answer) {
        console.log("app.vue emit dati", answer, index);
        if (this.quest.correct === index) {
          this.points++;
          console.log("bravo, giusta", this.points);
        }

        // console.log(this.quest.question);
        var asked = this.questions[this.block].questions.find(
          (el) => el.question === this.quest.question
        );
        console.log("filter works?", asked);

        const ind = this.questions[this.block].questions.indexOf(asked);

        if (ind > -1) {
          this.questions[this.block].questions.splice(ind, 1);
        }

        console.log(this.questions);

        if (this.questions[this.block].questions.length === 0) {
          this.block++;
        }

        // this.randomQuestion();
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
