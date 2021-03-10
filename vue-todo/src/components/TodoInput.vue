<template>
  <div class="inputBox shadow">
    <!--화면에서 입력되는 값이 저장되어 Vue 탭에서도 볼수있음-->
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <!--<button v-on:click="addTodo">add</button>-->
    <span class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      newTodoItem: ""
    }
  },
  methods: {
    addTodo: function() {
      if (this.newTodoItem !== '') {
        this.clearInput();
      }
    },
    clearInput: function() {
      this.$emit('addTodoItem', this.newTodoItem);  //addTodoItem 이벤트 발생시킴
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