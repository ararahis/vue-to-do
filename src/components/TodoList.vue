<template>
  <div>
    <div class="ui centered card">
      <div class="ui message">
        <div class="content">
          <a class="header">Управление</a>
          <div class="description">
          </div>
          <p>Законченые задачи: {{todos.filter(todo => {return todo.done === true}).length}}</p>
          <p>Осталось Задач: {{todos.filter(todo => {return todo.done === false}).length}}</p>
          </div>

        </div>
      </div>

    <todo v-on:complete-todo="completeTodo" v-on:update-todo="updateTodo" v-on:delete-todo="deleteTodo" v-for="(todo, index) in todos"  v-bind:key="index" v-bind:todo="todo"></todo>
  </div>
</template>

<script type = "text/javascript" >

  import Todo from './Todo';

  export default {
    props: ['todos'],
    components: {
      Todo
    },
    methods: {
      deleteTodo (todo) {
        const todoIndex = this.todos.indexOf(todo)
        this.todos.splice(todoIndex, 1)
      },
      completeTodo(todo) {
        const todoIndex = this.todos.indexOf(todo);
        this.todos[todoIndex].done = true;
      },
      updateTodo(todo) {
        const todoIndex = this.todos.indexOf(todo);
        this.$set( this.todos, todoIndex, todo )
      }
    }

  }
</script>
<style>
</style>
