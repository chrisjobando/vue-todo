<template>
  <div>
    <form @submit="addTodo">
      <input type="text" name="title" v-model="title" placeholder="Add Todo..." />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
import { v4 as uuidV4 } from 'uuid';

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

      if (this.title !== '') {
        const newTodo = {
          id: uuidV4(),
          completed: false,
          title: this.title
        };

        this.title = '';
        this.$emit('add-todo', newTodo);
      }
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
