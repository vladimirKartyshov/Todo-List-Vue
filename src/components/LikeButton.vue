<template> // исправлен коммит в git , для удобства проверки
  <div class="container">
    <div>
      <button class="ml" @mouseover="onHover" type="button" @click="counter++">
        &#9829; {{ counter }}
      </button>
    </div>
    <div>
      <button class="ml" @mouseover="onHover" type="button" @click="counter2--">
        &#9829; {{ counter2 }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppLikeButton',
  data() {
    return {
      counter: 0,
      counter2: 0,
    }
  },
  methods: {
    onHover: function (e) {
      e.target.style.color = 'red'
    },
  },
}
</script>

<style>
.container {
  display: flex;
}
.ml {
  margin-left: 5px;
}
</style>
