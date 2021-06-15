<template>
  <div>
    <h1>Database</h1>
    <div>Data List : </div>
    <ul>
      <li v-for="item in todos" :key="item">{{item.Name}}<button @click ="deleteTodo(item.Name)">-</button></li> 
    </ul>
    <input v-model="myText" type="text"/>
    <button @click="addTodos">Add Data</button>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    data:()=>{
      return {
        todos: [],
        myText:''
      }
    },
    mounted: function(){
      this.getTodos()
    },
    methods: {
      getTodos(){
        axios.get('http://localhost:3000/todo')
        .then(result => {
          this.todos = result.data
        })
      },
      addTodos(){
        let addItem = {Name: this.myText}
        axios.post('http://localhost:3000/todo', addItem)
        this.todos.push(addItem)
      },
      deleteTodo(Name){
        axios.delete(`http://localhost:3000/todo/${Name}`)
          .then(() => {
            this.getTodos()
        })
      }
    }
  }
</script>
