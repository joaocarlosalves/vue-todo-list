<template>
  <div class="home">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
  import Todos from './../components/Todos';
  import AddTodo from './../components/AddTodo';
  import axios from 'axios';

  export default {
    name: 'home',
    components: {
      AddTodo,
      Todos
    },
    data() {
      return {
        todos: []
      }
    },
    methods: {
      deleteTodo(id) {
        axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(this.todos = this.todos.filter(todo => todo.id != id))
        .catch(err => console.log(err));      
      },
      addTodo(newTodo) {
        const { title, completed } = newTodo;      

        axios.post('https://jsonplaceholder.typicode.com/todos', {
          title, completed
        })
        .then(res => this.todos = this.todos = [...this.todos, newTodo])
        .catch(err => console.log(err));
      }
    },
    created() {
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=30')
      .then(res => this.todos = res.data)
      .catch(err => console.log(err));
    }
  }
</script>
