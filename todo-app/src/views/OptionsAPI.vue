<script>
export default {
  name: "OptionsAPI",
  data() {
    return {
      todos: [],
      todo: "",
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length + 1,
        todo: this.todo,
        isDeleted: false,
      });
      this.todo = "";
    },
    deleteTodo(id) {
      const index = this.todos.findIndex((t) => t.id === id)
      this. todos[index].isDeleted = !this.todos[index].isDeleted
    }
  },
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
