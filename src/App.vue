<script setup>
import {ref} from 'vue'

let todos = ref(['A', 'B', 'C'])
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

</script>

<template>
  <h1>My Todo Application</h1>
  <ul>
    <li v-for="(todo, index) in todos">
      <input type="checkbox" v-model="todo.complete">
      
    <button @click="deleteTodo(index)">🗑️</button>
   
    {{ index }}
    {{ todo.text }} 
    </li>
  </ul>
  

    <input v-model="newTodo" @keydown.enter="addTodo">
    <button @click="addTodo" id="sumbitThing">Add Todo</button>

</template>


<style scoped>
header {
  line-height: 1.5;
}


.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>

