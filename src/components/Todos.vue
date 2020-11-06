<template>
  <div v-if="todos.length > 0">
    <div id="filters">
      <button
        id="active"
        @click="
          showActive = !showActive;
          showCompleted = false;
        "
        :class="{ checked: this.showActive }"
      >
        Active
      </button>
      <button
        id="completed"
        @click="
          showCompleted = !showCompleted;
          showActive = false;
        "
        :class="{ checked: this.showCompleted }"
      >
        Completed
      </button>
    </div>
    <p>
      {{ todos.filter((t) => !t.completed).length }}
      {{ todos.filter((t) => !t.completed).length > 1 ? "Tasks" : "Task" }}
      Remaining
    </p>
    <ul>
      <li :key="todo.id" v-for="todo in filteredTodos">
        <Todo
          :todo="todo"
          @delete="$emit('delete', todo.id)"
          @edit="$emit('edit')"
        />
      </li>
    </ul>
    <button
      @click="
        todos.forEach((t) => {
          if (t.completed) $emit('delete', t.id);
        })
      "
    >
      Clear Completed
    </button>
  </div>
</template>

<script>
import Todo from "./Todo";
export default {
  name: "Todos",
  components: {
    Todo,
  },
  props: ["todos"],
  data() {
    return {
      showCompleted: false,
      showActive: false,
    };
  },
  computed: {
    filteredTodos: function() {
      console.log(this.todos);
      let f = this.todos;
      if (this.showCompleted) f = f.filter((t) => t.completed);
      if (this.showActive) f = f.filter((t) => !t.completed);
      return f;
    },
  },
};
</script>

<style scoped>
#filters {
  display: flex;
  align-content: center;
  justify-content: center;
}

button {
  border: none;
  width: 45%;
  height: 35px;
  background: white;
  border-radius: 20px;
  font-size: 1.2rem;
  margin: 5px;
}

.checked {
  background: var(--background);
  color: #eee;
}

p {
  color: #333;
}

ul {
  list-style: none;
  padding: 0 10px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
}

li {
  flex-basis: 100%;
  min-height: 0;
}

@media screen and (min-width: 768px) {
  button {
    width: 30%;
  }

  p {
    font-size: 1.1rem;
  }

  li {
    flex-basis: 50%;
  }
}

@media screen and (min-width: 1200px) {
  button {
    width: 20%;
  }

  p {
    font-size: 1.2rem;
  }

  li {
    flex-basis: 33.3333%;
  }
}
</style>
