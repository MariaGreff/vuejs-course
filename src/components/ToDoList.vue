<template>
  <div>
    <ul>
      <ToDoItem v-for="todo of todos" v-bind:todo="todo" v-bind:key="todo" />
    </ul>
  </div>
</template>

<script>
import ToDoItem from "@/components/ToDoItem";
export default {
  props: ["todos"],
  components: {
    ToDoItem
  }
};
</script>
