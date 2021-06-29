# VMware CodeHouse 2021 Prework - Chapter 4

## Objective
We will modify the Vue scaffolding code to make it consume TODO API. 


## Install axios
Axios is a Javascript package allowing the Vue app to make HTTP request using [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). To install:
```
cd ~/src/codehouse-2021-prework/todo-vue
npm install axios
```

## Display todo items
First delete the file `todo-vue/src/components/HellowWorld.vue` since we are going to write our own todo UI. Modify the App.vue file to look like this:

```
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
    this.getList();
  },
  methods: {
    getList: getList
  }
}

function getList() {
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
```

In the template, the `v-for` directive loops through each item in the todos collection. The `getTodos()` method makes a GET request to our todo API at the url `/api/todos` . Build the Vue app and launch the Go app:

```
cd ~/src/codehouse-2021-prework/todo-vue

# rebuild the Vue app
rm -rf dist
npm run build

#launch the Go app
cd ..
go run .
```
Open a browser and navigate to http://localhost:8090. The todo list should display.

Note next time you make a change to the Vue app, you only need to re-build teh Vue app while keeps the Go app running.

## Add a form for adding todo
 
