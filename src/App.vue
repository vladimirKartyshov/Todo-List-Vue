<template>
  <div id="app">
    <h1>Список задач</h1>
    <div>Осталось сделать задач: <span class="counter">2</span></div>
    <div class="list">
      <div class="item done">
        <input type="checkbox" checked />
        Развернуть окружение в Codepen
      </div>
      <div class="item">
        <input type="checkbox" />
        Пройти курс по Vue
      </div>
      <div class="item">
        <input type="checkbox" />
        Сделать интернет-магазин на Vue
      </div>
    </div>
    <div class="form">
      <input />
      <button type="button">Добавить</button>
    </div>
  </div>
</template>

//First Skillbox study project 

<script>
export default {
  name: 'App',
}
</script>

<style scoped>
#app {
  background-color: powderblue;
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
}
.list {
  padding: 20px;
  border: 1px solid #ccc;
  margin: 20px 0;
  width: 300px;
}
.item {
  margin: 10px 0;
}
.done {
  text-decoration: line-through;
}
.form {
  margin: 20px 0;
}
</style>
