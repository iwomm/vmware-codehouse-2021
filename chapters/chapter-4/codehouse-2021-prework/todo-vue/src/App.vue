<template>
  <div id="app">
    <todo-list :todos="todos" />
  </div>
</template>

<script>
import axios from "axios";

import TodoList from '@/components/TodoList.vue'

const appData = {
  todos: []
}
  
export default {
  name: 'app',
  components: {
    TodoList
  },
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