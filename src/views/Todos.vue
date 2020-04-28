<template>
  <div>
    <router-link to="/">Home</router-link>
    <AddTodoForm @add-todo="addTodo"></AddTodoForm>
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="notCompleted">Not Completed</option>
    </select>
    <Loader v-if="loading"></Loader>
    <!-- @ = v-on -->
    <TodoList
      v-else-if="filteredTodos.length"
      @remove-todo="removeTodo"
      v-bind:todos="filteredTodos"
    ></TodoList>
    <p v-else>Nothing here</p>
  </div>
</template>

<script>
import TodoList from "../components/TodoList";
import AddTodoForm from "../components/AddTodoForm";
import Loader from "../components/Loader";
export default {
  name: "App",
  data() {
    return {
      todos: [],
      loading: true,
      filter: "all",
    };
  },
  components: {
    TodoList,
    AddTodoForm,
    Loader,
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
      .then((response) => response.json())
      .then((json) => {
        this.todos = json;
        this.loading = false;
      })
      .catch((err) => console.log(err.message));
  },
  watch: {
    filter(value) {
      console.log(value);
    },
  },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      }
      if (this.filter === "completed") {
        return this.todos.filter((t) => t.completed);
      }
      if (this.filter === "notCompleted") {
        return this.todos.filter((t) => !t.completed);
      }
    },
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter((t) => t.id !== id);
    },
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
  },
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
