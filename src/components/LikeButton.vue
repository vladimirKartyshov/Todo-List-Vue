<template>
  <div class="container">
    <div>
      <button
        class="ml"
        @mouseover="onHover"
        type="button"
        @click="increment()"
      >
        &#9829; {{ counter }}
      </button>
    </div>
    <div>
      <button
        class="ml"
        @mouseover="onHover"
        type="button"
        @click="discrement()"
      >
        &#9829; {{ counter2 }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppLikeButton',
  props: {
    counter: Number,
    counter2: Number,
  },

  // Одна из крутых фишек vue, нельзя мутировать props
  data() {
    // return {
    //   optimisticCounter: this.counter,
    //   optimisticCounter2: this.counter2,
    // }
  },

  methods: {
    // counterChange() {
    //   this.optimisticCounter++
    // },
    // counterChange2() {
    //   this.optimisticCounter2--
    // },

    // increment() {
    //   this.$emit('counter-change', this.counter + 1)
    // },
    increment() {
      this.$emit('update:counter', this.counter + 1)
    },
    // discrement() {
    //   this.$emit('counter-change2', this.counter2 - 1)
    // },
    discrement() {
      this.$emit('update:counter2', this.counter2 - 1)
    },
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
