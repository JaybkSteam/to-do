<script setup>
import {ref, watch} from 'vue'

let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ??[])
let newTodo = ref('')

function addTodo(){
  todos.value.push({
    text: newTodo.value,
    complete: false
  })

  newTodo.value = ''
}

function deleteTodo(index){
  todos.value.splice(index, 1)

}
watch(todos, function(value){
  console.log(value)
}, {deep: true})

watch(todos,function(value){
  window.localStorage.setItem('todos', JSON.stringify(value))
}, {deep: true})

 let filter = ref('all')

 function todoFilter (todo){
  if(filter.value =='active'){
    return todo.complete == false
  } else if (filter.value == 'completed'){
    return todo.complete == true
  } else {
    return true
  }
 }

</script>

<template>
  <h1>My Todo Application</h1>
  <ul>
    <input name="filter" type="radio" value="all" v-model="filter">
    <label>All</label>


    <input name="filter" type="radio" value="active" v-model="filter">
    <label>Active</label>

    <li v-for="(todo, index) in todos.filter(todoFilter)" :class="{completed: todo.complete}">
      <input type="checkbox" v-model="todo.complete">
      
    <button @click="deleteTodo(index)">🗑️</button>
   
    {{ index }}
    {{ todo.text }} 
    </li>
  </ul>
  

    <input v-model="newTodo" @keydown.enter="addTodo">
    <button @click="addTodo" id="sumbitThing">Add Todo</button>

   
    

</template>


<style>

body  {
    background: rgb(88,50,108);
background: linear-gradient(117deg, pink 20%, blue 100%);
font-family: 'Bruno Ace SC', cursive;

    min-height: 100vh;
}

</style>

