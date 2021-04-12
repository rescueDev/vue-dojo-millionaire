<template>
  <div id="app">
    <Popup v-if="isCorrect === false">
      <template v-slot:gameOver>
        <h2>Game Over</h2>
        <p>Please start a new game...</p>
      </template>
    </Popup>
    <Popup v-else-if="isCorrect === true">
      <template v-if="winner === false" v-slot:correct>
        <h2>Correct!! You win {{ dollars }} $</h2>
        <p>Next question is coming...</p>
      </template>
      <template v-else-if="winner === true" v-slot:correct>
        <h2>Congratulation You Are A Millionaire!!!</h2>
        <p>Now enjoy your money!!</p>
      </template>
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
      <div v-show="dollars !== 0" class="mt-2 btn btn-success">
        {{ dollars }} $
      </div>
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
        game: "",
        winner: false,
        quest: {
          question: "",
          answers: [],
        },
        block: 0,
        nQ: 0,
        points: 0,
        dollars: 0,
        isCorrect: null,
      };
    },
    methods: {
      startGame() {
        this.randomQuestion();
      },
      endGame() {
        this.game = "";
        this.quest = {
          question: "",
          answers: [],
        };
        this.block = 0;
        this.points = 0;
        this.dollars = 0;
        this.nQ = 0;
        this.isCorrect = null;
      },
      randomQuestion() {
        //set results style answers false
        this.$refs.containerComp.$children[1].clear();

        //get random block games 0-5
        var randomBlock = this.questions;

        // console.log("randomBlock", randomBlock);

        //check if block game is the same or new
        if (this.game === "") {
          this.game =
            randomBlock[
              Math.floor(Math.random() * randomBlock.length)
            ].questions;
        }

        // console.log("this game", this.game);

        //get first question of block
        const quest = this.game[this.nQ];

        //assign question, answers and correct
        this.quest = {
          question: quest.question,
          answers: quest.content,
          correct: quest.correct,
        };
        console.log("corretta", this.quest.correct);
      },

      checkAnswer(index, answer, results) {
        console.log("app.vue emit dati", answer, index, results);

        //check if correct answer
        if (this.quest.correct === index) {
          this.isCorrect = true;
          this.points++;

          //set correct dollars value for each question
          if (this.nQ >= 0 && this.nQ <= 3) {
            console.log("question: ", this.nQ);
            this.dollars += 500;
          } else if (this.nQ === 4) {
            console.log("blocco: ", this.nQ);

            this.dollars = 3000;
          } else if (this.nQ >= 5 && this.nQ <= 6) {
            console.log("question: ", this.nQ);

            this.dollars += 2000;
          } else if (this.nQ === 7) {
            console.log("question: ", this.nQ);

            this.dollars = 10000;
          } else if (this.nQ > 8 && this.nQ <= 9) {
            console.log("question: ", this.nQ);

            this.dollars += 5000;
          } else if (this.nQ === 10) {
            console.log("question: ", this.nQ);

            this.dollars = 30000;
          } else if (this.nQ === 11) {
            console.log("question: ", this.nQ);

            this.dollars = 70000;
          } else if (this.nQ === 12) {
            console.log("question: ", this.nQ);

            this.dollars = 150000;
          } else if (this.nQ === 13) {
            console.log("question: ", this.nQ);

            this.dollars = 300000;

            //if last question
          } else if (this.nQ === 14) {
            console.log("question: ", this.nQ);

            this.dollars = 1000000;

            this.winner = true;

            //dialog winner Millionaire
            setTimeout(() => {
              console.log("Winner!! You are a Milionaire!!");
              this.endGame();
            }, 7000);
          }

          // console.log("bravo, giusta", this.points);

          //pass to second and more questions (much difficult) until the last quest
          if (this.nQ < 15) {
            this.game[this.nQ++];
            console.log("domanda successiva", this.nQ);
            setTimeout(() => {
              this.isCorrect = null;
              this.randomQuestion();
              console.log("eseguo funzione");
            }, 3000);
          }

          //if not correct game over
        } else {
          // alert("game over!!");
          this.isCorrect = false;
          setTimeout(() => {
            this.endGame();
            console.log("game over, resetting data....");
          }, 2000);
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
