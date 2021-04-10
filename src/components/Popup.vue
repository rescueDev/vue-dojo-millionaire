<template>
  <dialog open>
    <slot></slot>
  </dialog>
</template>

<style scoped>
  dialog {
    position: fixed;
    top: 20vh;
    left: 10%;
    width: 50%;
    background-color: white;
    padding: 1rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  }
</style>
