<template>
  <div class="inputBox shadow">
    <!--화면에서 입력되는 값이 저장되어 Vue 탭에서도 볼수있음-->
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <!--<button v-on:click="addTodo">add</button>-->
    <span class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>
    <Modal v-if="showModal" @close="showModal = false"> 
      <!--
        you can use custom content here to overwrite
        default content
      -->
      <h3 slot="header">경고!</h3>
      <div slot="body">아무것도 입력하지 않으셨습니다.</div>
    </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  data: function() {
    return {
      newTodoItem: "",
      showModal: false  //기본값은 false로 설정
    }
  },
  methods: {
    addTodo: function() {
      if (this.newTodoItem !== '') {
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput: function() {
      this.$emit('addTodoItem', this.newTodoItem);  //addTodoItem 이벤트 발생시킴
      this.newTodoItem = '';
    }
  },
  components: {
    Modal: Modal  // @ES6기능@  Modal로 축약가능 (객체 속성명과 값명이 같음)
  }
}
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
</style>