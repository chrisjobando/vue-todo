<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import axios from 'axios';

import Todos from './components/Todos.vue';
import AddTodo from './components/AddTodo.vue';
import Header from './components/layout/Header.vue';

export default {
  name: 'App',
  components: { AddTodo, Header, Todos },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios
        .post('https://jsonplaceholder.typicode.com/todos', { title, completed })
        .then((res) => (this.todos = [...this.todos, res.data]))
        .catch((err) => console.log(err));
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id != id);
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(() => (this.todos = this.todos.filter((todo) => todo.id != id)))
        .catch((err) => console.log(err));
    }
  },
  created() {
    axios
      .get('https://jsonplaceholder.typicode.com/todos?_limit=20')
      .then((res) => (this.todos = res.data))
      .catch((err) => console.log(err));
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
