<template>
  <div id="app">
    <TodoHeader />
    <TodoInput @addTodo="addOneItem" />
    <TodoList
      :todoItems="todoItems"
      @toggleItem="toggleOneItem"
      @removeItem="removeOneItem" />
    <TodoFooter @clearAll="clearAllItem" />
  </div>
</template>

<script>
import { TodoHeader, TodoInput, TodoList, TodoFooter } from './components'

export default {
  name: 'app',
  data () {
    return {
      todoItems: []  
    }
  },
  methods: {
    addOneItem (todoItem) {
      const obj = { completed: false, item: todoItem };
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeOneItem (todoItem, index) {
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    },
    toggleOneItem (index) {
      const todoItem = this.todoItems[index];
      todoItem.completed = !todoItem.completed;
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItem () {
      localStorage.clear();
      this.todoItems = [];
    }
  },
  created () {
    if (localStorage.length) {
      for (let index = 0; index < localStorage.length; index ++) {
        const todoKey = localStorage.key(index);
        if (todoKey === 'loglevel:webpack-dev-server') { continue; }
        let todoItem = localStorage.getItem(todoKey);
        if (!todoItem) { continue; }
        todoItem = JSON.parse(todoItem);
        if (todoItem.item) { this.todoItems.push(todoItem); }
      }
    }
  },
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter
  }
}
</script>

<style>
body {
  text-align: center;
  background-color: #F6F6F6;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, .03);
}
</style>
