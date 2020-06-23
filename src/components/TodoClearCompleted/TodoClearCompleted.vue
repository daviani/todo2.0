<template >
  <button @click="clearCompleted"
          v-if="showClearCompletedButton" >
    Clear Completed
  </button >
</template >

<script >
  export default {
    name: 'todo-clear-completed',
    computed: {
      showClearCompletedButton() {
        return this.$store.getters.showClearCompletedButton;
      },
    },
    methods: {
      clearCompleted() {
        this.$store.dispatch('clearCompleted');
      },
    },
  };
</script >
