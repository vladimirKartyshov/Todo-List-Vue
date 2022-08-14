<template>
  <div id="app">
    <h1>Список задач</h1>
    <div>Осталось сделать задач: <span class="counter">2</span></div>
    <div class="list">
      <div class="item" v-for="(task, index) in tasks" :key="index">
        <input type="checkbox" checked />
        {{ task }}
      </div>
      <div class="item-done" v-for="(task, index) in tasks2" :key="index">
        <input type="checkbox" checked />
        {{ task }}
      </div>
    </div>
    <div class="form">
      <input :placeholder="message" />
      <button type="button" :disabled="isSubmitting">Добавить</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      message: 'Hello vue',
      isSubmitting: true,
      tasks: [
        'Развернуть окружение в Codepen',
        'Пройти курс по Vue',
        'Сделать интернет-магазин на Vue',
      ],
      tasks2: ['Начал курс vue skillbox', 'Купил пива', 'Покормил кота'],
    }
  },
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
.item-done {
  text-decoration: line-through;
  padding-top: 10px;
}
.form {
  margin: 20px 0;
}
</style>
