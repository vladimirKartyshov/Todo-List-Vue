<template>
  <div class="list">
    <h2 class="h2">{{ title }}</h2>
    <div
      class="item lkbtn"
      :class="{done: task.done}"
      v-for="task in tasks"
      :key="task.text"
    >
      <input type="checkbox" v-model="task.done" />
      {{ task.text }}
      <app-like-button
        v-model:counter="task.likes"
        v-model:counter2="task.disLikes"
      />
    </div>
  </div>
</template>

<script>
import AppLikeButton from './LikeButton.vue'

export default {
  name: 'AppTaskList',
  components: {
    AppLikeButton,
  },
  props: {
    tasks: [],
    title: String,
  },
}
</script>

<style>
.list {
  padding: 20px;
  border: 1px solid #ccc;
  margin: 20px 0;
  width: 400px;
}
.lkbtn {
  display: flex;
  align-items: center;
}

.item {
  margin: 10px 0;
}
.h2 {
  color: rgb(233, 81, 233);
  text-align: center;
}
</style>
