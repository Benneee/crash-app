<template>
  <div id="app">
    <AddToDo @add-to-do="addToDo" />
    <Todos :todos="todos" @del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddToDo from '../components/AddToDo';

import axios from 'axios';
export default {
  name: 'Home',
  components: {
    Todos,
    AddToDo,
  },
  data() {
    return {
      todos: [],
    };
  },

  methods: {
    deleteTodo(todoId) {
      if (confirm('Are you sure you want to delete this todo?'))
        axios
          .delete(`https://jsonplaceholder.typicode.com/todos/${todoId}`)
          .then((res) => {
            if (res) {
              this.todos = this.todos.filter((todo) => todo.id !== todoId);
            }
          })
          .catch((error) => console.log('error: ', error));
    },

    addToDo(newTodo) {
      const { title, completed } = newTodo;
      axios
        .post('https://jsonplaceholder.typicode.com/todos', {
          title,
          completed,
        })
        .then((res) => (this.todos = [...this.todos, res.data]))
        .catch((error) => console.log('error: ', error));
    },
  },

  created() {
    axios
      .get('https://jsonplaceholder.typicode.com/todos?_limit=10')
      .then((res) => (this.todos = res.data))
      .catch((error) => console.log('error: ', error));
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #333;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
