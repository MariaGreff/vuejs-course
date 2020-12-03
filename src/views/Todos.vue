<template>
  <div>
    <h3>TODO App</h3>
    <router-link to="/">Home</router-link>
    <AddToDo @add-todo="AddToDo" />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    <hr />
    <Loader v-if="loading" />
    <ToDoList
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
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
      loading: true,
      filter: "all"
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
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      }
      if (this.filter === "completed") {
        return this.todos.filter(t => t.completed);
      }
      if (this.filter === "not-completed") {
        return this.todos.filter(t => !t.completed);
      }
      return null;
    }
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
