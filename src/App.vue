<template>
  <div>
    <todo-list v-bind:todos="todos"></todo-list>
    <create-todo v-on:add-todo="addTodo" />
  </div>
</template>

<script>
import TodoList from './components/TodoList'
import CreateTodo from './components/CreateTodo.vue'

let todos_arr = [{
  title: 'Выучить Vue.js',
  project: 'Vue.js',
  done: false
}, {
  title: 'Выучить React.js',
  project: 'React.js',
  done: true,
}, {
  title: 'Выучить Angular 2',
  project: 'Angular 2',
  done: false
}, {
  title: 'Выучить Angular',
  project: 'Angular',
  done: false
}]

export default {
  name: 'app',
  components: {
    TodoList,
    CreateTodo
  },
  // Все данные использованные в данной функции можно будет вызывать в шаблоне
  data() {
    return {
      todos: localStorage.getItem('todos') ? JSON.parse(localStorage.getItem('todos')) : todos_arr
    }
  },
  methods: {
    addTodo (title) {
      this.todos.push({
        title: title.title,
        project: title.project,
        done: false
      })
      console.log('todos is', this.todos)
      //localStorage.setItem('todos', JSON.stringify(this.todos))
    }
  },
  created: function() {
    localStorage.setItem('todos', JSON.stringify(this.todos))
  },
  watch: {
    todos: function (val) {
      localStorage.setItem('todos', JSON.stringify(val))
    },
    deep: true
  }

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
