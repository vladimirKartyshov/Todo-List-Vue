<template>
  <div id="app">
    <div class="lkbtn">
      <h1 @mouseover="onHover2">Список задач</h1>
      <app-like-button></app-like-button>
    </div>

    <div v-if="count() == 0">Job well done</div>
    <div v-else-if="count() == 1">Осталась всего одна задача</div>
    <div v-else>
      Осталось сделать задач: <span class="counter">{{ count() }}</span>
    </div>
    <div class="list">
      <div
        class="item lkbtn"
        :class="{done: task.done}"
        v-for="(task, index) in tasks"
        :key="index"
      >
        <input type="checkbox" v-model="task.done" />
        {{ task.text }}
        <app-like-button></app-like-button>
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
    <div class="form lkbtn">
      <input @mouseover="onHover2" v-model="message" @keydown.enter="addTask" />
      <button type="button" @click="addTask" :disabled="isSubmitting">
        Добавить
      </button>
      <app-like-button></app-like-button>
    </div>
    <transition name="bounce">
      <img
        class="image"
        src="https://images.unsplash.com/photo-1509479200622-4503f27f12ef?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1169&q=80"
        v-show="count() == 0"
      />
    </transition>
  </div>
</template>

<script>
import AppLikeButton from './components/LikeButton.vue'
export default {
  name: 'App',
  components: {
    AppLikeButton,
  },
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
    onHover2: function (e) {
      e.target.style.color = 'green'
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
.lkbtn {
  display: flex;
  align-items: center;
}
.list {
  padding: 20px;
  border: 1px solid #ccc;
  margin: 20px 0;
  width: 400px;
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
/* .anm-enter {
  opacity: 0;
}
.anm-enter-active {
  animation: 3s anm-slide ;
  transition: opacity 8s;
}

.anm-leave-active {
  animation: 3s anm-slide ;
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
} */
.bounce-enter-active {
  animation: bounce-in 0.5s;
}

.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
    rotate: 0deg;
  }

  50% {
    transform: scale(1.5);
    rotate: 45deg;
  }

  100% {
    transform: scale(1);
    rotate: -45deg;
  }
}
</style>
