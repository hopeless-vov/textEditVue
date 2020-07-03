<template>
  <div id="app">
   <h2>Вводимо наш текст, змінюємо колір та бекграунд, нажимання на checkbox перекреслює текст(робить завдання виконаним); вибираємо колір та виділяємо наш текст, змінюємо розмір</h2>
        <router-link to ="/">Litle editor</router-link>

   <AddTodo
    @add-todo="addTodo"
   />
   <TodoList 
    v-if="todos.length"
    v-bind:todos ="todos"
    @remove-todo="removeTodo"
   />
   <p v-else>Поки немає записів</p>
 
  </div>
</template>

<script>
 import TodoList from '@/components/TodoList'
 import AddTodo from '@/components/AddTodo'
export default {
 
  data() {
    return {
      todos: [] 
      
    }
  },
   
  methods:{
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !==id)
    },
    addTodo(todo) {
        this.todos.push(todo)
          let json = JSON.stringify(todos);
            
         alert(json);
         
        
       
         
    } 
     
     
  
    
  },
  components: {
   TodoList, AddTodo
  }
}
</script>