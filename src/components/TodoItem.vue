<template>
  <div class="todo-item" v-bind:class="{ 'is-complete': todo.completed }">
    <p>
      <input type="checkbox" v-on:change="markComplete" />
      {{ todo.title }}
      <button class="del" @click="$emit('del-todo', todo.id)">x</button>
    </p>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: ['todo'],
  methods: {
    markComplete() {
      // eslint-disable-next-line vue/no-mutating-props
      this.todo.completed = !this.todo.completed;
    }
  }
};
</script>

<style lang="scss" scoped>
.todo-item {
  padding: 10px;
  background: #f4f4f4;
  border-bottom: 1px #ccc dotted;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  border: none;
  float: right;
  color: #fff;
  cursor: pointer;
  padding: 5px 9px;
  border-radius: 50%;
  background: #ff0000;
}
</style>
