<template>
  <div>
    <form @submit="addTodo">
      <input
        type="text"
        v-model="text"
        name="text"
        placeholder="Enter todo item..."
        maxlength="50"
      />
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script>
import { v4 } from "uuid";

export default {
  name: "AddTodo",
  data() {
    return {
      text: "",
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      if (this.text !== "") {
        const newTodo = {
          id: v4(),
          text: this.text,
          completed: false,
        };
        this.$emit("add", newTodo);
        this.text = "";
      }
    },
  },
};
</script>

<style scoped>
div {
  display: flex;
  justify-content: center;
  align-content: center;
}

form {
  width: 90%;
  display: flex;
  justify-content: space-between;
  align-content: center;
}

input {
  width: 80%;
  height: 40px;
  text-align: center;
  font-size: 1.3rem;
  border-radius: 20px;
  border: none;
}

button {
  border: none;
  width: 15%;
  background: white;
  border-radius: 20px;
  font-size: 1.2rem;
}

button:focus,
button:hover {
  background: skyblue;
}

@media screen and (min-width: 768px) {
  input {
    height: 50px;
    font-size: 1.5rem;
  }
}
</style>
