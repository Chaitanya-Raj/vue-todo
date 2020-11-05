<template>
  <div>
    <div v-if="todos.length > 0">
      <div id="filters">
        <button
          id="active"
          @click="
            active = !active;
            completed = false;
          "
          :class="{ checked: this.active }"
        >
          Active
        </button>
        <button
          id="completed"
          @click="
            completed = !completed;
            active = false;
          "
          :class="{ checked: this.completed }"
        >
          Completed
        </button>
      </div>
      <p>
        {{ todos.filter((t) => !t.completed).length }}
        {{ todos.filter((t) => !t.completed).length > 1 ? "Tasks" : "Task" }}
        Remaining
      </p>
    </div>
    <ul>
      <li :key="todo.id" v-for="todo in filteredTodos">
        <Todo
          :todo="todo"
          @delete="$emit('delete', todo.id)"
          @edit="$emit('edit')"
        />
      </li>
    </ul>
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
      completed: false,
      active: false,
    };
  },
  computed: {
    filteredTodos: function() {
      let f = this.todos;
      if (this.completed) f = f.filter((t) => t.completed);
      if (this.active) f = f.filter((t) => !t.completed);
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
