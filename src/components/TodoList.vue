<template>
  <div>
    <ul>
      <li v-for="todoItem in todoItems"
        :key="'todo-item-' + todoItem"
        class="shadow">
        {{todoItem}}
        <span class="removeBtn" @click="removeTodo">
          <i class="fas fa-trash-alt" />
        </span>
      </li>
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
  },
  methods: {
    removeTodo () { // 할 일 삭제 Func
    }
  }
}
</script>

<style scoped>
ul {
  margin-top: 0;
  padding-left: 0px;
  list-style-type: none;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: .5rem 0;
  padding: 0 .9rem;
  background: #fff;
  border-radius: 5px;
}
.checkBtn {
  margin-right: 5px;
  line-height: 45px;
  color: #62acde;
}
.checkBtnCompleted {
  color: #b3adad;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
</style>