<template>
  <div>
    <ul>
      <li :key="todo.id" v-for="todo in todos">
        <Todo :todo="todo" @delete="$emit('delete', todo.id)" />
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
};
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0 10px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
}

li {
  flex-basis: 100%;
}

@media screen and (min-width: 768px) {
  li {
    flex-basis: 33.3333%;
  }
}
</style>
