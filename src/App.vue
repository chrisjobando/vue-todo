<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from './components/Todos.vue';
import AddTodo from './components/AddTodo.vue';
import Header from './components/layout/Header.vue';

export default {
  name: 'App',
  components: { AddTodo, Header, Todos },
  data() {
    return {
      todos: [
        { id: 1, title: 'Task One', completed: false },
        { id: 2, title: 'Task Two', completed: true },
        { id: 3, title: 'Task Three', completed: false }
      ]
    };
  },
  methods: {
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id != id);
    }
  }
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  line-height: 1.4;
  font-family: Arial, Helvetica, sans-serif;
}

.btn {
  border: none;
  color: #fff;
  cursor: pointer;
  padding: 7px 20px;
  background: #555;
  display: inline-block;
}

.btn:hover {
  background: #666;
}
</style>
