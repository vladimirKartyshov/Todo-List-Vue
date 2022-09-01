<template>
  <div id="app">
    <div class="title-lkbtn">
      <h1 @mouseover="onHover2">Список задач</h1>
      <!-- <app-like-button
        :counter="headerLikes"
        :counter2="headerDisLikes"
        @counter-change="headerLikes = $event"
        @counter-change2="headerDisLikes = $event"
      ></app-like-button> -->
      <app-like-button
        v-model:counter="headerLikes"
        v-model:counter2="headerDisLikes"
      ></app-like-button>
      <h3>Общее количество лайков {{ countLikes }}</h3>
      <h3>Общее количество дизлайков {{ countDisLikes }}</h3>
    </div>

    <div v-if="count == 0">Job well done</div>
    <div v-else-if="count == 1">Осталась всего одна задача</div>
    <div v-else>
      Осталось сделать задач: <span class="counter">{{ count }}</span>
    </div>

    <app-task-list :tasks="uncompletedTasks" v-show="count >= 1">
    </app-task-list>

    <div class="form lkbtn">
      <input @mouseover="onHover2" v-model="message" @keydown.enter="addTask" />
      <button
        type="button"
        @click="addTask"
        :disabled="isSubmitting"
        v-if="countMessage <= 30"
      >
        Добавить
      </button>
      <app-like-button
        v-model:counter="formLikes"
        v-model:counter2="formDisLikes"
      ></app-like-button>
    </div>

    <transition name="bounce">
      <img
        class="image"
        src="https://images.unsplash.com/photo-1509479200622-4503f27f12ef?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1169&q=80"
        v-show="count == 0"
      />
    </transition>

    <div>
      <app-task-list :tasks="completedTasks" :title="title"></app-task-list>
    </div>
  </div>
</template>

<script>
import AppLikeButton from './components/LikeButton.vue'
import AppTaskList from './components/TaskList.vue'

export default {
  name: 'App',
  components: {
    AppLikeButton,
    AppTaskList,
  },

  data() {
    return {
      headerLikes: 2,
      headerDisLikes: 0,
      formLikes: 3,
      formDisLikes: 0,
      title: 'Заверешенные задачи',
      message: 'Hello vue',
      isSubmitting: false,
      tasks: [
        {
          text: 'Развернуть окружение в Codepen',
          done: false,
          likes: 0,
          disLikes: 0,
        },
        {
          text: 'Пройти курс по Vue, Skilbox-schl',
          done: false,
          likes: 3,
          disLikes: 0,
        },
        {
          text: 'Сделать интернет-магазин на Vue',
          done: false,
          likes: 4,
          disLikes: 0,
        },
      ],
    }
  },

  computed: {
    countMessage() {
      return this.message.length
    },
    count() {
      return this.tasks.filter((task) => !task.done).length
    },
    completedTasks() {
      return this.tasks.filter((task) => task.done)
    },
    uncompletedTasks() {
      return this.tasks.filter((task) => !task.done)
    },
    countLikes() {
      return (
        this.headerLikes +
        this.formLikes +
        this.tasks.reduce((value, task) => value + task.likes, 0)
      )
    },
    countDisLikes() {
      return (
        this.headerDisLikes +
        this.formDisLikes +
        this.tasks.reduce((value, task) => value + task.disLikes, 0)
      )
    },
  },

  methods: {
    addTask() {
      this.tasks.push({text: this.message, done: false, likes: 0, disLikes: 0})
      this.message = ''
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

.title-lkbtn {
  display: flex;
  align-items: center;
  flex-direction: column;
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
