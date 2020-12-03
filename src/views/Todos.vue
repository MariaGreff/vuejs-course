<template>
  <div>
    <h3>TODO App</h3>
    <router-link to="/">Home</router-link>
    <hr />
    <AddToDo @add-todo="AddToDo" />
    <ToDoList v-bind:todos="todos" @remove-todo="removeToDo" />
  </div>
</template>

<script>
import ToDoList from "@/components/ToDoList";
import AddToDo from "@/components/AddToDo";
export default {
  name: "App",
  data() {
    return {
      todos: []
    };
  },
  components: {
    ToDoList,
    AddToDo
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
      .then(response => response.json())
      .then(json => {
        this.todos = json;
      });
  },
  methods: {
    removeToDo(id) {
      this.todos = this.todos.filter(t => t.id !== id);
    },
    AddToDo(todo) {
      this.todos.push(todo);
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
