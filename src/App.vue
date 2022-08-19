<template>
  <div id="app">
    <h1 @mouseover="onHover">Список задач</h1>
    <div v-if="count() == 0">Job well done</div>
    <div v-else-if="count() == 1">Осталась всего одна задача</div>
    <div v-else>
      Осталось сделать задач: <span class="counter">{{ count() }}</span>
    </div>
    <div class="list">
      <div
        class="item"
        :class="{done: task.done}"
        v-for="(task, index) in tasks"
        :key="index"
      >
        <input type="checkbox" v-model="task.done" />
        {{ task.text }}
      </div>
      <!-- <div
        class="item"
        :class="{done: task.done}"
        v-for="(task, index) in tasks2"
        :key="index"
      >
        <input type="checkbox" v-model="task.done" />
        {{ task.text }}
      </div> -->
    </div>
    <div class="form">
      <input @mouseover="onHover" v-model="message" @keydown.enter="addTask" />
      <button type="button" @click="addTask" :disabled="isSubmitting">
        Добавить
      </button>
    </div>
    <transition name="anm">
      <img
        class="image"
        src="https://images.unsplash.com/photo-1509479200622-4503f27f12ef?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1169&q=80"
        v-show="count() == 0"
      />
    </transition>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      message: 'Hello vue',
      isSubmitting: false,
      tasks: [
        {text: 'Развернуть окружение в Codepen', done: true},
        {text: 'Пройти курс по Vue', done: false},
        {text: 'Сделать интернет-магазин на Vue', done: false},
      ],
      // tasks2: [
      //   {text: 'Начал курс vue skillbox', done: false},
      //   {text: 'Купил пива и креветки', done: true},
      //   {text: 'Покормил кота', done: true},
      // ],
    }
  },
  methods: {
    addTask() {
      this.tasks.push({text: this.message, done: false})
      this.message = ''
    },
    count() {
      return this.tasks.filter((task) => !task.done).length
    },
    onHover: function (e) {
      e.target.style.color = 'red'
    },
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
.done {
  text-decoration: line-through;
}
.form {
  margin: 20px 0;
}
.image {
  width: 500px;
}
.anm-enter {
  opacity: 0;
}
.anm-enter-active {
  transition: opacity 8s;
}
/* .anm-enter-to {
  animation: 3s anm-slide;
} */
/* .anm-leave {
  animation: 3s anm-slide backwards;
} */
.anm-leave-active {
  animation: 3s anm-slide forwards;
  transition: opacity 1s;
}
.anm-leave-to {
  opacity: 0;
}
@keyframes anm-slide {
  from {
    transform: translateX(0px);
  }
  to {
    transform: translateX(-100px);
  }
}
</style>
