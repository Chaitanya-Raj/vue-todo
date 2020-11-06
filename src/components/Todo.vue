<template>
  <div :class="{ completed: todo.completed }">
    <p contenteditable @blur="editTodo" v-html="todo.text"></p>
    <button @click="markComplete" id="done">✔</button>
    <button @click="$emit('delete', todo.id)" id="delete">✖</button>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: ["todo"],
  methods: {
    markComplete() {
      const editedTodo = { ...this.todo, completed: !this.todo.completed };
      this.$emit("edit", editedTodo);
    },
    editTodo(e) {
      const editedTodo = { ...this.todo, text: e.target.innerHTML };
      this.$emit("edit", editedTodo);
    },
  },
};
</script>

<style scoped>
.completed {
  background: #333;
}

.completed > p {
  text-decoration: line-through;
  opacity: 0.5;
}

.completed > button {
  background: #111;
  color: #eee;
}

div {
  margin: 5px 5px;
  height: 4rem;
  display: flex;
  align-items: center;
  border-radius: 20px;
  padding-left: 20px;
  padding-right: 5px;
  background: var(--background);
  flex-grow: 1;
  animation: fade-in 1s;
}

@keyframes fade-in {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

p {
  color: var(--text);
  word-wrap: break-word;
  /* word-break: break-all; */
  padding-right: 15px;
  text-align: left;
}

button {
  height: 2rem;
  width: 2rem;
  margin: 10px;
  background: #fff;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  flex-shrink: 0;
}

#done {
  margin-left: auto;
}

@media screen and (min-width: 768px) {
  div {
    height: 9.5rem;
    margin: 10px;
    font-size: 1.3rem;
  }

  p {
    padding: 10px;
    flex-grow: 1;
    text-align: center;
  }

  button {
    font-size: 1.3rem;
    height: 2rem;
    width: 2rem;
  }
}
</style>
