<template>
  <div>
    <!--<app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header>-->
    <app-header 
      v-bind:propsdata="str"
      v-on:renew="renewStr">  <!--AppHeader에서 보낸 이벤트를 받는 곳-->
    </app-header>
    <h1>{{ propsdata }}</h1>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue';
//new Vue({
//  data: {
//    str: 'hi' // 불가능
//  }
//})

export default {
  props: ['propsdata'],
  data: function() { //함수로 반환값을 주는 형태 가능
    return{
      str: 'Header'
    }
  },
  components: {
    'app-header': AppHeader
  },
  methods: {
    renewStr: function() {
      this.str = 'hi';
    }
  }
}
</script>

<style>
</style>
