# VMware CodeHouse 2021 Prework- Chapter 3

## Objective
We will add UI to the Go project using the Vue.js framework. 


## Required tools before start
- [Install nodejs and npm](https://nodejs.org/en/download/)
- Install vue-cli using npm by running command:

	`npm install -g @vue/cli`


## Scaffold the vue-todo project

Run the following command in a terminal:
```
cd ~/src/codehouse-2021-prework
vue create todo-vue
```
Select `Default ([Vue 2] babel, eslink)` from the command-line options using the up/down arrow keys and the enter key. We choose Vue 2.x instead of Vue 3.x because many current learning materials are still for Vue 2, and most concept2 from Vue 2 still apply to Vue 3.

The last command created a subfolder named `vue-todo` under your project folder. Next run these commands in the terminal:
```
cd todo-vue
npm serve
```
This launched another web app on local port 8081. Open a browser and navigate to http://localhost:8081. The "Welcome to Your Vue.js App" page will display.

## Combine the API and the vue projects together
To make things simpler, we will embed the Vue project in the Go project, and serve requests to both parts from the same port (8090).

In the previous terminal, first stop the Vue server launched from the last step (ctrl+C), then run the following commands:
```
rm -rf dist
npm run build
```
This compiled the Vue project and saved the result in the `dist` folder, which contains the static contents (html/css/image/js) for browser to run. To serve this static content from the Go app, run the following commands in terminal:
```
cd ~/src/codehouse-2021-prework
go get github.com/gin-contrib/static
```
In VS Code, edit the main.go file to add a new import:

`	"github.com/gin-contrib/static"
`

and add a new route url ('/') before the API endpoint handlers:
  
`	r.Use(static.Serve("/", static.LocalFile("./todo-vue/dist", false))) 
`

The new main.go should look like:

```
package main

import (
	"net/http"
	"strconv"

	"github.com/gin-contrib/static"
	"github.com/gin-gonic/gin"
)

var nextId int = 0
var todos []Todo

func GetNextId() int {
	value := nextId
	nextId++
	return value
}

func GetTodos(c *gin.Context) {
	c.JSON(http.StatusOK, gin.H{"list": todos})
}

func PostTodo(c *gin.Context) {
	var item Todo
	if err := c.ShouldBindJSON(&item); err != nil {
		c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
		return
	}

	item.Id = GetNextId()
	todos = append(todos, item)
	c.String(http.StatusCreated, c.FullPath()+"/"+strconv.Itoa(item.Id))
}

func DeleteTodo(c *gin.Context) {
	idString := c.Param("id")

	if id, err := strconv.Atoi(idString); err == nil {
		for index := range todos {
			if todos[index].Id == id {
				todos = append(todos[:index], todos[index+1:]...)
				c.Writer.WriteHeader(http.StatusNoContent)
				return
			}
		}
	}

	c.JSON(http.StatusBadRequest, gin.H{"error": "invalid id"})
}

func main() {
	todos = append(todos, Todo{Id: GetNextId(), Value: "CodeHouse", DueDate: "7/31/2021"})

	r := gin.Default()
	r.Use(static.Serve("/", static.LocalFile("./todo-vue/dist", false)))
	r.GET("/api/todos", GetTodos)
	r.POST("/api/todos", PostTodo)
	r.DELETE("/api/todos/:id", DeleteTodo)
	r.Run(":8090")
}
```

Use the `go run .` comamnd to run the Go app, then open the browser to navigate to http://localhost:8090. You should now see the same "Welcome to Your Vue.js App" page. 

Now the Go app is serving the Vue contents. We will modify the Vue scaffolding app to consume the TODO API in the next chapter.




