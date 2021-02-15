<template>
  <div>
    <form @submit.prevent="addTodo">
      <input
        type="text"
        v-model="title"
        name="title"
        placeholder="Add Todo..."
      />
      <input type="submit" class="btn" value="Submit" />
    </form>
  </div>
</template>

<script>
// import { v4 as uuidv4 } from 'uuid';
export default {
  name: 'AddToDo',
  data() {
    return {
      title: '',
    };
  },

  methods: {
    addTodo() {
      const newToDo = {
        title: this.title,
        completed: false,
      };

      this.$emit('add-to-do', newToDo);
      this.title = '';
    },
  },
};
</script>

<style lang="css" scoped>
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
