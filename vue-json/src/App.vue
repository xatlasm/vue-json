<template>
  <div id="app">
    <h1>{{title}}</h1>
    <button v-on:click="getTodos">Get todo list</button>
    <ol v-if="todos" id="todo-list">
      <li v-for="todo in todos" v-bind:key="todo.id">
        <p>{{todo.name}}</p>
      </li>
    </ol>
  </div>
</template>

<script>
import axios from 'axios'
const baseURL = 'https://api.myjson.com/bins/jebvm'
export default {
  data() {
    return {
      title: "Todo List",
      todos: null
    }
  },
  methods: {
    getTodos() {
      axios.get(baseURL)
        .then(response => {
          this.todos = response.data.todos
        })
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
