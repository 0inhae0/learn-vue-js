<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" 
      v-on:removeItem="removeOneItem" 
      v-on:toggleItem="toggleOneItem"></TodoList>
    <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data: function() {
    return {
      todoItems: []
    }
  },
  methods:{
  // Todoinput에서 옮겨옴, this.newTodoItem → todoItem을 인자로 받기 때문에 모두 바꿈
  // 할일을 추가하고 엔터를 쳤을 때, 바로 화면에 나타나도록 함
    addOneItem: function(todoItem) {
      // 텍스트 + 텍스트가 저장됐는지 안됐는지에 대한 진위값(Boolean 값)
      var obj = {completed: false, item: todoItem};
      //console.log(this.newTodoItem);
      // 저장하는 로직
      localStorage.setItem(todoItem, JSON.stringify(obj)); // 객체인 obj를 string으로 변환시켜줌
      this.todoItems.push(obj);
    },
    removeOneItem: function(todoItem, index) {
      // slice - 기존 배열을 변경하지 않고 지움 , splice - 새로운 배열을 반환  
      this.todoItems.splice(index, 1);
      // 설정값 바꿈
        //todoItem.completed = !todoItem.completed;
      // 로컬 스토리지의 데이터를 갱신
      localStorage.removeItem(todoItem.item);
        //localStorage.setItem(index, 1);
    },
    toggleOneItem: function(todoItem, index){
      // 설정값 바꿈 , 1번과 2번이 같은 동작을 하지만 2번이 컴포넌트 간의 경계를 좀 더 명확히 한다
        //todoItem.completed = !todoItem.completed; //1
      this.todoItems[index].completed = !this.todoItems[index].completed; //2
      // 로컬 스토리지의 데이터를 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItems: function() {
      localStorage.clear();
      this.todoItems = [];
    }
  },
  // TodoList에서 옮겨옴
  created: function() {
    if(localStorage.length > 0) {
      for(var i = 0; i < localStorage.length ; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server'){
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
          //this.todoItems.push(localStorage.key(i));
        }
      }
    }
  },
  components: {
    //컴포넌트 태그명: 컴포넌트 내용
    'TodoHeader': TodoHeader,
    'TodoInput': TodoInput,
    'TodoList': TodoList,
    'TodoFooter': TodoFooter
  }
}
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f6;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)
}
</style>
