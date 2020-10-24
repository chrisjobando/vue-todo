<template>
  <div>
    <form @submit="addTodo">
      <input type="text" name="title" v-model="title" placeholder="Add Todo..." />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
import uuid from 'uuid';

export default {
  name: 'AddTodo',
  data() {
    return {
      title: ''
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();

      const newTodo = {
        id: uuid.v4(),
        completed: false,
        title: this.title
      };

      this.title = '';
      this.$emit('add-todo', newTodo);
    }
  }
};
</script>

<style lang="scss" scoped>
form {
  display: flex;
}

input[type='text'] {
  flex: 10;
  padding: 5px;
}

input[type='submit'] {
  flex: 2;
}
</style>
