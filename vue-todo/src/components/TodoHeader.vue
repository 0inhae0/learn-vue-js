<template>
  <div>
    <h1>TO DO it!</h1>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
/* 원래는 상위의 HTML 요소의 스타일을 상속받게 되는데, 이때 scoped(싱글파일 컴포넌트)를 사용하게 되면 이 컴포넌트 안에서만 유효하게 됨*/
  h1 {
    color: #2f3b52;
    font-weight: 900;
    margin: 2.5rem 0 1.5rem;
  }
</style>