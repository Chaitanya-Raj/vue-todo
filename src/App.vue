<template>
  <div id="app">
    <h1>TodoList</h1>
    <AddTodo @add="addTodo" />
    <Todos :todos="todos" @delete="deleteTodo" @edit="editTodo" />
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
      this.editTodo();
    },
    editTodo() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    deleteTodo(todoId) {
      this.todos = this.todos.filter((todo) => todo.id !== todoId);
      this.editTodo();
    },
  },
};
</script>

<style>
* {
  outline: none;
  box-sizing: border-box;
}

:root {
  --background: #253a52;
  --text: #eee;
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
  border-radius: 20px;
}

h1 {
  background: var(--background);
  color: var(--text);
  margin: 0;
  margin-bottom: 30px;
  padding: 20px;
}
</style>
