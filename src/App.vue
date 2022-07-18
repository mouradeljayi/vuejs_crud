<template>
  <div class="container mt-5">
    <form @submit.prevent="addTodo">
      <div class="form-group">
        <input v-model="title" type="text" placeholder="Enter title" class="form-control">
      </div>
      <button type="submit" class="btn btn-primary">save</button>
    </form>
    <hr>
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        {{ todo.title }}
      </li>
    </ul>

  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  data() {
    return {
      title: '',
      todos: {}
    }
  },
  mounted() {
    axios.get('http://localhost:8000/todos/')
    .then(res => {
      this.todos = res.data
    }).catch(err => {
      console.log(err)
    })
  },
  methods: {
    addTodo() {
      axios.post('http://localhost:8000/todos/', {title: this.title})
      .then(res => {
        console.log(res)
      }).catch(err => {
        console.log(err)
      })
    }
  }
 
}
</script>

<style>

</style>
