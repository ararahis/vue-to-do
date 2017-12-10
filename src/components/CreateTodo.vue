<template>
  <div class='ui basic content center aligned segment'>
    <button class='ui basic button icon' v-on:click="openForm" v-show="!isCreating">
      <i class='plus icon'></i>
    </button>
    <div class='ui centered card' v-show="isCreating">
      <div class='content'>
        <div class='ui form'>
          <div class='field'>
            <label>Название</label>
            <input v-model="titleText" type='text' ref='title' defaultValue="">
          </div>
          <div class='field'>
            <label>Проект</label>
            <input v-model="projectText" type='text' ref='project' defaultValue="">
          </div>
          <div class='ui two button attached buttons'>
            <button class='ui basic blue button' v-on:click="sendForm()">
              Создать
            </button>
            <button class='ui basic red button' v-on:click="closeForm">
              Отменить
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        titleText: '',
        projectText: '',
        isCreating: false
      }
    },
    methods: {
      openForm () {
        this.isCreating = true
      },
      closeForm () {
        this.isCreating = false
      },
      sendForm () {
        this.$emit('add-todo', {
          title: this.titleText,
          project: this.projectText,
          done: false
        })
        this.newTodoText = ''
        this.isCreating = false
      }
    }
  }
</script>
