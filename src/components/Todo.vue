<template>
  <div>
    <h1>Database</h1>
    <div>Data List : </div>
    <ul>
      <li v-for="item in todos" :key="item">{{item.Name}}<button @click ="deleteTodos(item.Name)">-</button></li> 
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
      const username = localStorage.getItem('usr')
      const password = localStorage.getItem('pwd')
      axios.get('http://localhost:3000/todo', {headers:{username, password}} )
      .then(result => {
        this.todos = result.data
      })
    },
    addTodos(){
      const username = localStorage.getItem('usr')
      const password = localStorage.getItem('pwd')
      let addItem = {Name: this.myText}
      axios.post('http://localhost:3000/todo', addItem,  {headers:{username, password}} )
      this.todos.push(addItem)
    },
    deleteTodos(Name){
      const username = localStorage.getItem('usr')
      const password = localStorage.getItem('pwd')
      axios.delete(`http://localhost:3000/todo/${Name}`, {headers:{username, password}} )
        .then(() => {
          this.getTodos()
        })
    }
  }
  }
</script>
