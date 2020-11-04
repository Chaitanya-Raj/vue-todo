<template>
  <div id="app">
    <h1>TodoList</h1>
    <AddTodo @add="addTodo" />
    <Todos :todos="todos" @delete="deleteTodo" />
  </div>
</template>

<script>
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";
export default {
  name: "app",
  components: {
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")) || [],
    };
  },
  methods: {
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    deleteTodo(todoId) {
      this.todos = this.todos.filter((todo) => todo.id !== todoId);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style>
* {
  outline: none;
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
  font-family: Verdana, Geneva, sans-serif;
  min-height: 100vh;
}

#app {
  min-height: 100vh;
  text-align: center;
  background: #ddd;
}

h1 {
  background: #333;
  color: #eee;
  margin: 0;
  margin-bottom: 30px;
  padding: 20px;
}
</style>
