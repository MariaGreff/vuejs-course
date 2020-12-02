<template>
  <div id="app">
    <h2>TODO App</h2>
    <ToDoList v-bind:todos="todos" @remove-todo="removeToDo" />
  </div>
</template>

<script>
import ToDoList from "@/components/ToDoList";
export default {
  name: "App",
  data() {
    return {
      todos: [
        { id: 1, title: "Buy bread", completed: false },
        { id: 2, title: "Buy milk", completed: false },
        { id: 3, title: "Buy cookies", completed: false }
      ]
    }
  },
  components: {
    ToDoList
  },
  methods: {
    removeToDo(id) {
      this.todos = this.todos.filter(t => t.id !== id);
    }
  }
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
