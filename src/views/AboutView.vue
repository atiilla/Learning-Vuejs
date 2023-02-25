<template>
  <main>
    <h1>About</h1>
    <p>This is the about page.</p>
    <button @click="handleClick">Click me</button>
    <p>{{ state.count }}</p>
    <p>{{ state.todo.title }}</p>
    <button @click="()=>GetTodoById(5)">Get Todo</button>

    <ul>
        <li v-for="todo in state.todos" :key="todo.id">
            {{ todo.title }}
        </li>
    </ul>
  </main>
</template>

<script>
// state management
import { reactive } from "vue";

const handleClick = () => {
  return state.count++;
};

const GetTodoById = (id)=>{
    fetch(`https://jsonplaceholder.typicode.com/todos/${id}`)
    .then(response => response.json())
    .then(json => {
        state.todo = json
    })
    .catch(err => {
        console.log(err)
    })
}

const GetAllTodos = ()=>{
    fetch('https://jsonplaceholder.typicode.com/todos')
    .then(response => response.json())
    .then(json => {
        state.todos = json
    })
    .catch(err => {
        console.log(err)
    })
}

const state = reactive({
  count: 0,
  todo: {},
  todos: []
});

export default {
mounted(){
  
    fetch('https://jsonplaceholder.typicode.com/todos/1')
    .then(response => response.json())
    .then(json => {
        console.log(json)
        state.todo = json
    })
    .catch(err => {
        console.log(err)
    })

    GetAllTodos()
},
  methods: {
    handleClick,
    GetTodoById,
    GetAllTodos
  },
  data() {
    return {
      message: "Hello World",
    };
  },
  setup() {
    return {
      state,
    };
  },
};
</script>

<style>
</style>