<template>
  <div>
    <Question />
    <Answer />
  </div>
</template>

<script>
  import Question from "@/components/Question.vue";
  import Answer from "@/components/Answer.vue";
  export default {
    components: {
      Answer,
      Question,
    },
  };
</script>
