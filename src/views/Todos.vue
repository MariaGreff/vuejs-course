<template>
  <div>
    <h3>TODO App</h3>
    <router-link to="/">Home</router-link>
    <AddToDo @add-todo="AddToDo" />
    <hr />
    <Loader v-if="loading" />
    <ToDoList
      v-else-if="todos.length"
      v-bind:todos="todos"
      @remove-todo="removeToDo"
    />
    <p v-else>No todos</p>
  </div>
</template>

<script>
import ToDoList from "@/components/ToDoList";
import AddToDo from "@/components/AddToDo";
import Loader from "@/components/Loader";
export default {
  name: "App",
  data() {
    return {
      todos: [],
      loading: true
    };
  },
  components: {
    ToDoList,
    AddToDo,
    Loader
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
      .then(response => response.json())
      .then(json => {
        this.todos = json;
        this.loading = false;
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
