<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos  v-bind:todos="todos" v-on:del-todo="deleteTodo"/> <!-- Det etter semikolon kan være hva som helst, 
    det i hermetegn må reffere til det inne i data. Dette blir da sendt inn som en "Prop" -->

  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios';  // Using axios instead of fetch to get json data

export default {
  name: 'Home',
  components: {
    // HelloWorld
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(id) { // Deletes the todo with the specified id
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res =>  this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err => console.log(err)); 
    },
    addTodo(newTodo) { // Adds the new todo to the end of the list of todos
      const { title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos',{ title, completed }) // Make a post and gets back a todo complete with an id.
      .then(res => this.todos = [...this.todos, res.data])
      .catch(err => console.log(err));
    }
  },
  created() { // Gets json data from the url. The get method returns a promise.
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=15').then(res => this.todos = res.data).catch(err => console.log(err));
  }

}
</script>

<style>
/*
#app {
   font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px; 
  }*/

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  } 

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: #666;
  }

</style>
