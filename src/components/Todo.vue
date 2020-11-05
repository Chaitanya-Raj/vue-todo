<template>
  <div @click="markComplete" :class="{ completed: todo.completed }">
    <p>
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
      this.$emit("edit");
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
  background: #aaa;
}

div {
  margin: 10px 5px;
  display: flex;
  align-items: center;
  border-radius: 20px;
  padding-left: 20px;
  padding-right: 5px;
  background: var(--background);
  cursor: pointer;
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
  animation: fade-in 2s;
  text-align: left;
}

button {
  height: 20px;
  margin: 10px;
  border: none;
  border-radius: 50%;
  margin-left: auto;
  flex-shrink: 0;
}

@media screen and (min-width: 768px) {
  div {
    height: 150px;
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
