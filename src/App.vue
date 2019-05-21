<template>
  <div id="app">
    <h1>{{title}}</h1>
    <button v-on:click="getTodos">Load todo list</button>
    <button v-on:click="clearTodos">Clear todo list</button>
    <form v-on:submit.prevent="newTodo">
      <input type="text" v-model="newTodoName" placeholder="New Todo">
    </form>
    <ul id="todo-list">
      <li v-for="todo in todos" v-bind:key="todo.id">
        <p>{{todo.name}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
const baseURL = 'https://api.myjson.com/bins/jebvm'
export default {
  data() {
    return {
      title: "Todo List",
      todos: []
    }
  },
  methods: {
    getTodos() {
      axios.get(baseURL)
        .then(response => {
          this.todos = response.data
        })
    },
    newTodo() {
      this.todos.push({
        id: this.todos.length + 1,
        name: this.newTodoName
      })
      this.newTodoName = ''
    },
    clearTodos() {
      this.todos = []
    }
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
#todo-list {
  text-align: left;
  font-weight: bold;
}
</style>
