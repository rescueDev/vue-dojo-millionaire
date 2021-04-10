<template>
  <div id="app">
    <Popup v-if="isCorrect === false">
      <h2>Game Over</h2>
      <p>Please start a new game...</p>
    </Popup>
    <img alt="Millionaire logo" src="./assets/logo.png" />
    <div class="mb-4">
      <button
        class="mt-3 btn btn-primary"
        v-show="quest.question === ''"
        @click="startGame"
      >
        Start Game
      </button>
    </div>
    <Container
      :question="quest.question"
      :answers="quest.answers"
      :correct="quest.correct"
      @check-answer="checkAnswer"
      ref="containerComp"
    >
    </Container>
  </div>
</template>

<script>
  import Container from "@/components/Container.vue";
  import Popup from "@/components/Popup.vue";
  import questions from "@/questions";

  export default {
    name: "App",
    components: {
      Container,
      Popup,
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
        isCorrect: null,
      };
    },
    mounted() {
      console.log("Refs", this.$refs.containerComp.$children[1].clear());
    },

    methods: {
      startGame() {
        this.randomQuestion();
      },
      endGame() {
        this.questions = questions;
        this.quest = {
          question: "",
          answers: [],
        };
        this.block = 0;
        this.points = 0;
        this.isCorrect = null;
      },
      randomQuestion() {
        //set results style answers false
        this.$refs.containerComp.$children[1].clear();

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

        //check if correct answer
        if (this.quest.correct === index) {
          this.isCorrect = true;
          this.points++;
          console.log("bravo, giusta", this.points);

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

          //passing next question if
          setTimeout(() => {
            this.randomQuestion();
            console.log("eseguo funzione");
          }, 4000);
        } else {
          // alert("game over!!");
          this.isCorrect = false;
          setTimeout(() => {
            this.endGame();
            console.log("game over, resetting data....");
          }, 4000);
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
