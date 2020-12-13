<template>
  <div>
    <ul>
      <li v-for="todoItem in todoItems"
        :key="'todo-item-' + todoItem">{{todoItem}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data () {
    return {
      todoItems: []
    }
  },
  created () {
    if (localStorage.length) {
      for (let index = 0; index < localStorage.length; index ++) {
        const todoItem = localStorage.key(index);
        if (todoItem === 'loglevel:webpack-dev-server') { continue; }
        this.todoItems.push(todoItem);
      }
    }
  }
}
</script>

<style scoped>

</style>