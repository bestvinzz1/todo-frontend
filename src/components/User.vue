<template>
  <div>
    <h1>Database</h1>
    <div>User List : </div>
    <ul>
      <li v-for="item in users" :key="item">{{item.Name}}<button @click ="deleteUser(item.Name)">-</button></li> 
    </ul>
    <input v-model="username"/>
    <input v-model="password"/>
    <button @click="Add">Add Data</button>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    data:()=>{
      return {
        users: [],
        username: '',
        password: ''
      }
    },
    mounted: function(){  
      this.getUsers()
    },
    methods: {
      getTodos(){
        axios.get('http://localhost:3000/user')
        .then(result => {
          this.users = result.data
        })
      },
      addTodos(){
        let addItem = {Name: this.myText}
        axios.post('http://localhost:3000/user', addItem)
        this.users.push(addItem)
      },
      deleteTodo(Name){
        axios.delete(`http://localhost:3000/user/${Name}`)
          .then(() => {
            this.getUsers()
        })
      }
    }
  }
</script>
