<template >
  <div >
    <label >
      <input :checked="!anyRemaining"
             @change="allChecked"
             type="checkbox" >
      Check All
    </label >
  </div >
</template >

<script >
  export default {
    name: 'todo-check-all',
    computed: {
      anyRemaining() {
        return this.$store.getters.anyRemaining;
      },
    },
    methods: {
      allChecked() {
        this.$store.dispatch('checkAll', event.target.checked);
      },
    },
  };
</script >
