<template>
  <div class="full space" ref="space">
    <div class="cam full">
      <button @click="makeFanScroller">Run</button>
      <button @click="reload">reload</button>
      <div :key="item.id" class="card" v-for="item in items" ref="itemset">
        {{ item.quote }}
      </div>
      <div ref="widther"></div>
    </div>
  </div>
</template>

<script>
import anime from 'animejs'
export default {
  data () {
    return {
      items: [
        {
          id: `_${Math.random()}`,
          quote: 'quote1'
        },
        {
          id: `_${Math.random()}`,
          quote: 'quote2'
        },
        {
          id: `_${Math.random()}`,
          quote: 'quote3'
        },
        {
          id: `_${Math.random()}`,
          quote: 'quote4'
        },
        {
          id: `_${Math.random()}`,
          quote: 'quote5'
        },
        {
          id: `_${Math.random()}`,
          quote: 'quote6'
        },
        {
          id: `_${Math.random()}`,
          quote: 'quote7'
        },
        {
          id: `_${Math.random()}`,
          quote: 'quote8'
        },
        {
          id: `_${Math.random()}`,
          quote: 'quote9'
        },
        {
          id: `_${Math.random()}`,
          quote: 'quote10'
        }
      ]
    }
  },
  methods: {
    makeFanScroller () {
      let spaceR = this.$refs['space'].getBoundingClientRect()
      let widther = this.$refs['widther']
      widther.style.width = `${spaceR.width * 0.5 + 300 / 2 + 400 * 10}px`
      widther.style.height = `1px`
      let tl = this.tl = anime.timeline()
      let step1 = {
        targets: this.$refs['itemset']
      }
      tl.add({
        ...step1,
        opacity: 0,
        elasticity: 50,
        rotateZ (el, i, n) {
          return (i - 0.5 * n) / n * 67
        },
        rotateY (el, i, n) {
          return 15
        },
        delay (el, i, n) {
          return i * 10
        },
        duration: 0
      })
      tl.add({
        ...step1,
        opacity: 1,
        elasticity: 50,
        translateY: -250 + spaceR.height * -0.2,
        translateX (el, i, n) {
          return (i - 0.5 * n) / n * 800
        },
        rotateZ (el, i, n) {
          return (i - 0.5 * n) / n * 67
        },
        rotateY (el, i, n) {
          return 15
        },
        delay (el, i, n) {
          return i * 50
        },
        duration: 1500
      })
      tl.add({
        ...step1,
        opacity: 1,
        elasticity: 50,
        translateY: -250 + spaceR.height * -0.2,
        translateX (el, i, n) {
          return i * 400 - 200
        },
        rotateZ (el, i, n) {
          return 0
        },
        rotateY (el, i, n) {
          return 0
        },
        duration (el, i, n) {
          return 300 * (n - i)
        },
        delay (el, i, n) {
          return 100
        }
      })
    },
    reload () {
      window.location.reload()
    }
  }
}
</script>

<style scoped>
.space{
  perspective: 100vmax;
  overflow: auto;
  -webkit-overflow-scrolling: touch;
}
.cam{
  transform-style: preserve-3d;
}

.card{
  opacity: 0;
  position: absolute;
  bottom: 0;
  left: calc(50% - 300px / 2);
  width: 300px;
  height: 300px;
  text-align: center;
  background-color: rgba(255,255,255,0.5);
  border: grey solid 1px;
  padding: 30px;
}
</style>
