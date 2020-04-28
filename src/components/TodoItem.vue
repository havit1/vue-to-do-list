<template>
  <li>
    <span v-bind:class="{ done: todo.completed }">
      <input
        v-on:change="todo.completed = !todo.completed"
        type="checkbox"
        name
        id
      />
      <strong>{{ index + 1 }}</strong>
      {{ todo.title | upperCase }}
    </span>
    <button v-on:click="$emit('remove-todo', todo.id)" class="rm">
      &times;
    </button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: Number,
  },
  filters: {
    upperCase(value) {
      return value.toUpperCase();
    },
  },
};
</script>

<style scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 0.2rem;
  margin-bottom: 1rem;
}
.rm {
  background-color: red;
  color: #fff;
  border-radius: 50%;
  font-weight: bold;
}

input {
  margin-right: 1rem;
}

.done {
  text-decoration: line-through;
}
</style>
