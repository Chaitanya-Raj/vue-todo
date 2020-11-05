<template>
  <div>
    <form @submit.prevent="addTodo">
      <input
        type="text"
        v-model="text"
        name="text"
        placeholder="Enter todo items..."
        maxlength="120"
      />
      <!-- <button type="submit">Add</button> -->
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
    addTodo() {
      if (this.text.trim() !== "") {
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
  margin-bottom: 10px;
}

form {
  width: 90%;
  display: flex;
  justify-content: space-between;
  align-content: center;
}

input {
  width: 100%;
  height: 40px;
  text-align: center;
  font-size: 1.3rem;
  border-radius: 20px;
  border: none;
}

@media screen and (min-width: 768px) {
  input {
    height: 50px;
    font-size: 1.5rem;
  }
}
</style>
