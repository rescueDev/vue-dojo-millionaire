<template>
  <div>
    <ul>
      <li v-for="answer in answers" :key="answer">
        {{ answer }}
      </li>
    </ul>
  </div>
</template>

<script>
  // import questions from "@/questions";
  export default {
    data() {
      return {};
    },
    props: {
      answers: Array,
    },
    // inject: ["prova"],
  };
</script>
