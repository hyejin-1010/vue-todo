<template>
  <div>
    <transition-group name="list" tag="ul">
      <li v-for="(todoItem, index) in todoItems"
        :key="'todo-item-' + todoItem.item" class="shadow">
        <i class="fas fa-check checkBtn"
          :class="{'checkBtnCompleted': todoItem.completed}"
          @click="toggleComplete(index)"></i>
        <span :class="{'textCompleted': todoItem.completed}">{{todoItem.item}}</span>
        <span class="removeBtn" @click="removeTodo(todoItem.item, index)">
          <i class="fas fa-trash-alt" />
        </span>
      </li>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: {
    todoItems: Array
  },
  methods: {
    removeTodo (todoItem, index) {
      this.$emit('removeItem', todoItem, index);
    },
    toggleComplete (index) {
      this.$emit('toggleItem', index);
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
.textCompleted {
  color: #b3adad;
  text-decoration-line: line-through;
}
.checkBtnCompleted {
  color: #b3adad;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}

/* 리스트 아이템 트랜지션 효과 */
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>