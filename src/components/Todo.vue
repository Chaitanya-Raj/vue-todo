<template>
  <div @click="markComplete">
    <p :class="{ completed: todo.completed }">
      {{ todo.text }}
    </p>
    <button @click="$emit('delete', todo.id)"><b>X</b></button>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    },
  },
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}

div {
  margin: 10px 5px;
  display: flex;
  align-items: center;
  border-radius: 20px;
  padding-left: 20px;
  padding-right: 5px;
  background: #333;
  cursor: pointer;
}

p {
  color: #eee;
  word-wrap: break-word;
  word-break: break-all;
  padding-right: 15px;
}

button {
  height: 20px;
  margin: 10px;
  border: none;
  border-radius: 50%;
  margin-left: auto;
}

@media screen and (min-width: 768px) {
  div {
    height: 100px;
    margin: 10px;
    font-size: 1.3rem;
  }

  button {
    font-size: 1.3rem;
    height: 2rem;
    width: 2rem;
  }
}
</style>
