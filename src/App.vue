<template>
  <div id="app">
    <h1>{{title}}</h1>
    <button @click="loadTodos(jsonKey)">Load todo list</button>
    <button @click="saveTodos(jsonKey)">Save todo list</button>
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
const baseURL = 'https://api.myjson.com/bins/'
export default {
  data() {
    return {
      title: "Todo List",
      todos: [],
      jsonKey: "jebvm"
    }
  },
  methods: {
    loadTodos(jsonKey) {
      jsonKey = prompt("Enter your key", jsonKey)
      if (jsonKey === null || jsonKey === '') {return}
      axios.get(baseURL+jsonKey)
        .then(response => {
          this.todos = response.data
          this.jsonKey = jsonKey
        })
    },
    saveTodos(jsonKey) {
      if (this.jsonKey === "jebvm" || this.jsonKey === '' || this.jsonKey === null) {
        axios.post(baseURL,this.todos)
          .then(response => {
            this.jsonKey = response.data.uri.match(/bins\/\/(.*)/)[1]
            alert("List saved successfully. Your key is:\n\n" + this.jsonKey + "\n\nPlease keep your key safe as you need it to load your list again.\nCaution: Anyone who knows your key can access your list!")
          })
      }
      else {
        axios.put(baseURL+jsonKey,this.todos)
          .then(response => {
            if (response.status===200) {
              alert("List saved successfully. Your key is:\n\n" + this.jsonKey + "\n\nPlease keep your key safe as you need it to load your list again.\nCaution: Anyone who knows your key can access your list!")
          }})
      }
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
