<template>
  <div>
    <p class="tasks">Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</p>
    <p class="tasks">In-Progress Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</p>
    <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo"
    v-for="todo in todos" :key="todo.title" :todo.sync="todo"></todo>
  </div>
</template>

<script>
import sweetalert from 'sweetalert';
import Todo from './Todo';

export default {
  props: ['todos'],
  components: {
    Todo,
  },
  methods: {
    deleteTodo(todo) {
      sweetalert({
        title: 'Are you sure?',
        text: 'This To-Do will be permanently deleted!',
        type: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#DD6B55',
        confirmButtonText: 'Yes, do it!',
        closeOnConfirm: false,
      },
      () => {
        const todoIndex = this.todos.indexOf(todo);
        this.todos.splice(todoIndex, 1);
        sweetalert('Deleted!', 'success');
      }); 
    },
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
      sweetalert('Success!', 'To-Do completed!', 'success');
    },
  },
};
</script>

<style>
  p.tasks {
    text-align: center;
  }
</style>
