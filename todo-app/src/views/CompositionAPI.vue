<script setup>
import {reactive, ref} from "vue";

const todos = reactive([])
const todo = ref("")

const addTodo = () => {
  todos.push({
    id: todos.length + 1,
    todo: todo.value,
    isDeleted: false
  })
  todo.value = ""
}

const deleteTodo = (id) => {
  const index = todos.findIndex((t) => t.id === id)
  todos[index].isDeleted = !todos[index].isDeleted
}

</script>

<template>
  <div class="app">
    <h1>Todo App</h1>
    <form @submit.prevent="addTodo">
      <input type="text" placeholder="Todos" v-model="todo">
      <button>Add Todo</button>
    </form>
    <ul>
      <li v-for="t in todos" :key="t.id" :class="{ completed: t.isDeleted }">
        <p>{{ t.todo }}</p>
        <div class="buttons">
          <button @click="deleteTodo(t.id)">{{ t.isDeleted ? "Undelete" : "Delete" }}</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .app {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 50px;
    font-family: Arial, sans-serif;
  }

  .completed {
    text-decoration: line-through;
    background: #5C805BF7;
    color: #dbefd6;
  }

  ul {
    width: 40%;
    height: 25%;
    display: flex;
    flex-direction: column;
    gap: 20px;
    list-style: none;
  }

  li {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    background: #9ac999;
    padding: 0 30px;
    border-radius: 5px;
  }

  button {
    padding: 10px 20px;
    color: #3e3e46;
    background: #88b2df;
    margin: 10px;
    border: none;
    border-radius: 5px;
  }
</style>
