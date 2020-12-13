<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" @keyup.enter="addTodo" />
    <span class="addContainer" @click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>
  </div>
</template>

<script>
export default {
  data () {
    return {
      newTodoItem: ""
    }
  },
  methods: {
    addTodo () {
      localStorage.setItem(this.newTodoItem, this.newTodoItem);
      this.clearInput();
    },
    clearInput () {
      this.newTodoItem = '';
    }
  }
}
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  height: 50px;
  line-height: 50px;
  background: #fff;
  border-radius: 5px;
}
.inputBox input {
  font-size: .9rem;
  border-style: none;
}
.addContainer {
  float: right;
  display: block;
  width: 3rem;
  background: linear-gradient(to right, #6478FB, #8763FB);
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: #fff;
  vertical-align: middle;
}
</style>