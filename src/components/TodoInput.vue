<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" @keyup.enter="addTodo" />
    <span class="addContainer" @click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>

    <Modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">
        경고!
        <i class="closeModalBtn fas fa-times" @click="showModal = false" />
      </h3>
      <div slot="body">
        아무것도 입력하지 않으셨습니다.
      </div>
    </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal'

export default {
  data () {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo () {
      if (!this.newTodoItem) { return this.showModal = !this.showModal; }
      this.$emit('addTodo', this.newTodoItem);
      this.clearInput();
    },
    clearInput () {
      this.newTodoItem = '';
    }
  },
  components: {
    Modal
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
.closeModalBtn {
  color: #42b983;
}
</style>