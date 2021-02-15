<template>
  <div>
    <div :key="todo.id" v-for="todo in todos">
      <Todoitem :todo="todo" @del-todo="$emit('del-todo', todo.id)" />
    </div>
  </div>
</template>

<script>
import Todoitem from './Todoitem.vue';

export default {
  name: 'Todos',
  components: {
    Todoitem,
  },
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped></style>
