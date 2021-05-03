<template>
  <h1>Todo List</h1>
  <button @click="createTodo" id="createTodoBtn">Create Todo</button>
  <div id="todos">
    <div v-for="todo in todos" :key="todo.id">
      <Todo
        :title="todo.title"
        :finished="todo.finished"
        :id="todo.id"
        @deleteTodo="deleteTodo"
        @toggleFinished="toggleFinished"
      />
    </div>
  </div>
</template>

<script>
import Todo from "./components/Todo";

import { v4 as uuid } from "uuid";

export default {
  name: "App",
  components: { Todo },
  data() {
    return { todos: null };
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos")) || [];
  },
  methods: {
    createTodo() {
      let todo = {
        title: prompt("Todo Title"),
        finished: false,
        id: uuid(),
      };
      if (todo.title.length > 25) {
        let titleArray = todo.title.split("");
        let newTitle = [];
        titleArray.forEach((titleSplit, index) => {
          if (index + 1 < 25) {
            newTitle.push(titleSplit);
          }
        });
        todo.title = newTitle.join("");
      }
      this.todos.push(todo);
      this.save();
    },
    deleteTodo(id) {
      let todos = this.todos.filter((todo) => todo.id != id);
      this.todos = todos;
      this.save();
    },
    toggleFinished(id) {
      let todos = this.todos;
      let todo = todos.filter((todo) => todo.id === id)[0];
      let i = todos.indexOf(todo);
      console.table([todos, todo, i]);

      todo.finished = !todo.finished;
      todos[i] = todo;
      this.todos = todos;
      this.save();
    },
    save() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#todos {
  list-style: none;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-end;
  padding: 10px;
}
#createTodoBtn {
  border: 0;
  color: white;
  background: #2c3e50;
  border-radius: 15px;
  text-align: center;
  padding: 5px;
}
body {
  margin: 0;
}
</style>
