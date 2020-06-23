<template >
  <div >
    <input @keyup.enter="addTodo" class="todo-input" placeholder="What needs to be done" type="text" v-model="newTodo" >
    <transition-group enter-active-class="animated fadeInUp" leave-active-class="animated fadeOutDown" name="fade" >
      <todo-item :checkAll="!anyRemaining" :key="todo.id" :todo="todo" v-for="todo in todosFiltered" />

    </transition-group >

    <div class="extra-container" >
      <todo-check-all />
      <todo-items-remaining />
    </div >

    <div class="extra-container" >
      <todo-filtered />

      <div >
        <transition name="fade" >
          <todo-clear-completed />
        </transition >
      </div >
    </div >
  </div >
</template >

<script >
  import TodoItem from '../TodoItem/TodoItem';
  import TodoItemsRemaining from '../TodoItemsRemaining/TodoItemsRemaining';
  import TodoCheckAll from '../TodoCheckAll/TodoCheckAll';
  import TodoFiltered from '../TodoFiltered/TodoFiltered';
  import TodoClearCompleted from '../TodoClearCompleted/TodoClearCompleted';

  export default {
    name: 'todo-list',
    components: {
      TodoItem,
      TodoItemsRemaining,
      TodoCheckAll,
      TodoFiltered,
      TodoClearCompleted,
    },
    data() {
      return {
        newTodo: '',
        idForTodo: 3,
      };
    },
    computed: {
      anyRemaining() {
        return this.$store.getters.anyRemaining;
      },
      todosFiltered() {
        return this.$store.getters.todosFiltered;
      },
    },
    methods: {
      addTodo() {
        if (this.newTodo.trim().length === 0) {
          return;
        }
        this.$store.dispatch('addTodo', {
          id: this.idForTodo,
          title: this.newTodo,
        });
        this.newTodo = '';
        this.idForTodo++;
      },
    },
  };
</script >


<style >
  @import url("https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css");

  .todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 16px;
  }

  .todo-input:focus {
    outline: 0;
  }

  .todo-item {
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    animation-duration: 0.2s;
  }

  .remove-item {
    cursor: pointer;
    margin-left: 14px;
  }

  .todo-item-left {
    display: flex;
    align-items: center;
  }

  .todo-item-label {
    padding: 10px;
    border: 1px solid white;
    margin-left: 12px;
  }

  .todo-item-edit {
    font-size: 24px;
    color: #2c3e50;
    margin-left: 12px;
    width: 100%;
    padding: 10px;
    border: 2px solid #ccc;
  }

  .todo-item-edit:focus {
    outline: none;
  }

  .completed {
    text-decoration: line-through;
    color: grey;
  }

  .extra-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 16px;
    border-top: 1px solid lightgrey;
    padding-top: 14px;
    margin-bottom: 14px;
  }

  button {
    border-width: 0;
    outline: none;
    border-radius: 2px;
    box-shadow: 0 1px 4px rgba(0, 0, 0, .6);
    background-color: white;
    margin: 5px;
    padding: 10px;
    font-weight: bold;
  }


  button :focus {
    background: #41B883;
  }

  button :hover {
    background: #1c543c;
  }

  .active {
    background: #41B883;
    color: white;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }

  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
</style >
