<template>
  <div class="hello" alig='center'>
    <h1>Todo List</h1>
    <form @submit.prevent="createpost">
      <div>
        <label for="title"></label>
        <input text="text" id="title" v-model="formData.title">
      </div>
      <button>add</button>
    </form>
  <div v-for="arr in array" :key=arr.id >
    
    <!--<input type="checkbox" v-model="uncheck" />-->
    <h3>{{arr.id}}. {{arr.title}}
    <button v-on:click="del(index)">
      Delete
    </button>
    <button v-on:click="edit(index)">
      Edit
    </button>
    </h3>
  </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
  data(){
    return{
      formData:{
        id: 0,
        title:'',
        completed: false
      },
      array : []
    }
    
  },
  methods:{
    check()
    {
      return this.task.length()<0 ? true : false;
    },
    createpost(){
      // eslint-disable-next-line no-unused-vars
      axios.post(`http://localhost:7275/api/Todos`,{ params: { id: 0, Title: this.title, completed: true }})
      .then((response)=>console.log(response))
      .catch((error)=>console.log(error))
    },
    del(index){
      this.array.splice(index,1)
    },
    edit(){
       
    },
  },
  async mounted()
  {
    axios.get(`https://localhost:7275/api/Todos`)
    .then((response)=>{
      console.log(response.data)
      this.array=response.data
    })
    .catch((error)=>{
      console.log(error)
    })
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
button{
   background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 8px 15px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 9px;
  border-radius: 9px;
}
</style>