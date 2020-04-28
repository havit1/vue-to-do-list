<template>
  <form @submit.prevent="onSumit">
    <input v-model="title" type="text" name id />
    <button type="submit">Create</button>
  </form>
</template>


<script>
export default {
  data() {
    return {
      title: ""
    };
  },
  methods: {
    onSumit() {
      if (this.title.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          completed: false
        };

        this.$emit("add-todo", newTodo);
        this.title = "";
      }
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
}

input {
  width: 400px;
}
</style>