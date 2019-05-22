<template>
  <div id="app">
    <h1>{{title}}</h1>
    <button @click="getTodos">Load todo list</button>
    <form v-on:submit.prevent="newTodo">
      <input type="text" v-model="newTodoName" placeholder="New Todo">
      <button type="submit">Create</button>
    </form>
    <button @click="clearTodos">Clear todo list</button>
    <ul id="todo-list">
      <li v-for="todo in todos" :key="todo.id" :class="todo.class">
        <p><input :id="todo.name" type="checkbox"><label :for="todo.name">{{todo.name}}</label> <button @click="deleteTodo(todo)">Delete</button></p>
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
      todos: [],
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
        name: this.newTodoName,
      })
      this.newTodoName = ''
    },
    clearTodos() {
      this.todos = []
    },
    deleteTodo(todo) {
      this.todos.splice(this.todos.indexOf(todo),1)
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
  list-style: none;
}
</style>
