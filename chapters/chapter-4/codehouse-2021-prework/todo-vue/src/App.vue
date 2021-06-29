<template>
  <div id="app">
    <h1>To-Do List</h1>
    <table>
      <tbody>
        <tr v-for="todo in todos" :key="todo.id">
          <td>{{ todo.value }}</td>
          <td>{{ todo.due_date }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";

const appData = {
  todos: []
}

export default {
  name: 'App',
  data() {
    return appData;
  },
  mounted: function() {
    this.getTodos();
  },
  methods: {
    getTodos: getTodos
  }
}

function getTodos() {
  axios.get("/api/todos").then( res => {
    appData.todos = res.data.list
  });
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin-top: 50px;
}
</style>