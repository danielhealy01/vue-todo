<template>
  <h1>Vue TODO</h1>
  <form 
    class="appThing"
    @submit.prevent="addTodo"
    >
    <input 
      placeholder="Add a todo..."
      type="text"
      v-model="newTodoContent"
    >
    <button
      :disabled="!newTodoContent"
    >Add</button>
  </form>
  <div class="cardContainer">
    <div 
      class="card"
      v-for="todo in todos"
      >
      <span>{{ todo.content }}</span>
      <button
      @click="deleteTodo(todo.id)"
      >Delete</button>
    </div>
  </div>
</template>



<script setup>

  import { ref } from 'vue'
  import { v4 as uuidv4 } from 'uuid'

  const todos = ref([
    // {
    //   id: 'id1',
    //   content: 'content',
    //   done: false,    
    // },
    // {
    //   id: 'id2',
    //   content: 'content2',
    //   done: false,
    // },
  ])

  const newTodoContent = ref('')
  
const addTodo = () => {
  const newTodo = {
    id: uuidv4(),
    content: newTodoContent.value,
    done: false,
  }
  console.log('new todo ' + newTodo.id)

  todos.value.unshift(newTodo)

  newTodoContent.value = ''

}

const deleteTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id)
} 

</script>