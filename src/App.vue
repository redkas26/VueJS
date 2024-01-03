<template>
  <div class="wrapper">
    <h1>Todo List</h1>
    <div>
      <form class="inputField" @submit.prevent="create">
        <input v-model="newTodo" autocomplete="off">
         <button>Ajouter</button> 
      </form>
    </div>
    <ul class="todoList">
        <li v-for="item in todos" :key="item.id">
            <h3 :class="{ done : item.completed }" @click="completed(item)">{{ item.content }}</h3>
            <button @click="remove(item)">Supprimer</button>
        </li>
    </ul>
    <div class="footer">
        <button @click="Marquer">Marquer tout</button>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const todos = ref([])
    const newTodo = ref('')

    function create() {
      todos.value.push({
        id: Date.now(),
        content: newTodo.value,
        completed: false
      })
      newTodo.value = ''
    }

    function remove(item){
      todos.value.splice(todos.value.indexOf(item), 1)
    }

    function completed(item){
      item.completed = !item.completed
    }

    function Marquer(){
      todos.value.forEach((Todo) => Todo.completed = true);
    }

    return {
      todos,
      newTodo,
      create,
      remove,
      completed,
      Marquer
    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  font-family: 'Poppins', sans-serif;
}
body{
  width: 100%;
  height: 100vh;
  /* padding: 10px; */
  background: rgb(131,58,180);
background: linear-gradient(90deg, rgba(131,58,180,1) 0%, rgba(253,29,29,1) 50%, rgba(252,176,69,1) 100%);
}
.wrapper{
  background: #fff;
  max-width: 400px;
  width: 100%;
  margin: 120px auto;
  padding: 25px;
  border-radius: 5px;
  box-shadow: 0px 10px 15px rgba(0,0,0,0.1);
}
.wrapper h1{
  color: rgb(0, 38, 255);
  text-align: center;

}
input{
  width: 97%;
  margin: 20px 0;
  height: 100%;
  border-radius: 3px;
  border: 1px solid #ccc;
  font-size: 17px;
  padding: 15px 5px;
  transition: all 0.3s ease;
}
form button {
  width: 97%;
  height: 100%;
  border: none;
  color: #fff;
  margin-left: 5px;
  font-size: 21px;
  outline: none;
  cursor: pointer;
  border-radius: 3px;
  /* pointer-events: none; */
  transition: all 0.3s ease;

  padding: 6px 10px;
  background: rgb(63,94,251);
background: radial-gradient(circle, rgba(63,94,251,1) 0%, rgba(252,70,107,1) 100%);
}
.wrapper .todoList{
  margin-top: 22px;
  max-height: 250px;
  overflow: auto;
}
.todoList button{
  padding: 3px;
  border: none;
  color: #fff;
  /* margin-left: 5px; */
  outline: none;
  cursor: pointer;
  border-radius: 3px;
  border: none;
  background: rgb(63,94,251);
background: radial-gradient(circle, rgba(63,94,251,1) 0%, rgba(252,70,70,1) 0%);
}
li{
  position: relative;
  list-style: none;
  margin-bottom: 8px;
  background: #d3d3d3;
  border-radius: 3px;
  padding: 11px 15px;
  cursor: default;
  overflow: hidden;
  word-wrap: break-word;
}
.footer{
  display: flex;
  width: 100%;
  margin-top: 20px;
  align-items: center;
  justify-content: space-between;
}
.footer button{
  padding: 6px 10px;
  border-radius: 3px;
  border: none;
  color: #fff;
  background: rgb(63,94,251);
background: rgba(63,94,251,1);
  cursor: pointer;
}
.item{
  cursor: pointer;
}
.done{
  text-decoration: underline;
}

</style>
