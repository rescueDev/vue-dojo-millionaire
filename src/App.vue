<template>
  <div id="app">
    <img alt="Millionaire logo" src="./assets/logo.png" />
    <div>
      <button @click="startGame">Start Game</button>
    </div>
    <Container :question="quest.question" :answers="quest.answers"> </Container>
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
    // provide() {
    //   return {
    //     prova: this.prova,
    //   };
    // },

    data() {
      return {
        questions: questions,
        // question: "",
        // answers: [],
        quest: {
          question: "",
          answers: [],
        },
        block: 0,
        prova: "",
      };
    },

    methods: {
      startGame() {
        this.randomQuestion();
      },
      randomQuestion() {
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
        };
        this.prova = random;
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
