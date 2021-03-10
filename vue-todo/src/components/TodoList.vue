<template>
  <div>
    <ul>
      <!--텍스트만 중복되지 않으면 이 키가 유일하기 때문에, v-for에 성능을 가속화 시키는 v-bind:key 연결-->
      <li v-for="(todoItem,index) in propsdata" v-bind:key="todoItem.item" class="shadow">
        <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" 
          v-on:click="toggleComplete(todoItem, index)"></i>
        <span v-bind:class="{textCompleted:todoItem.completed}">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['propsdata'],
  methods: {
    removeTodo: function(todoItem, index) {
      // removeItem이라는 이벤트 발생시켜, todoItem, index를 인자로 보냄
      this.$emit('removeItem', todoItem, index);
    },
    toggleComplete: function(todoItem, index) {
      // toggleItem이라는 이벤트 발생시켜, todoItem, index를 인자로 보냄
      this.$emit('toggleItem', todoItem, index);
    }
  }
}
</script>

<style>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  border-radius: 5px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
</style>