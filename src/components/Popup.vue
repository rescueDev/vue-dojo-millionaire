<template>
  <dialog open>
    <slot name="gameOver"></slot>
    <slot name="correct"></slot>
  </dialog>
</template>

<style scoped>
  dialog {
    position: fixed;
    top: 20vh;
    left: 5%;
    width: 30%;
    background-color: white;
    padding: 1rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  }
</style>
