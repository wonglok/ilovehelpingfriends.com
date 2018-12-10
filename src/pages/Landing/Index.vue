<template>
  <div class="full space" ref="space">
    <div class="cam full">
      <button @click="makeFanScroller">Run</button>
      <button @click="reload">reload</button>

      <div class="center">
        <div :key="item.id" class="card" v-for="item in items" ref="itemset">
          {{ item.letter }}
        </div>
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
      ]
    }
  },
  mounted () {
    this.populate()
  },
  methods: {
    populate () {
      let getID = () => `_${Math.random()}`
      let stringArr = `ilovehelpingfriends.com`.split('')

      this.items = stringArr.map((l) => {
        return {
          id: getID,
          letter: l
        }
      })
    },
    makeFanScroller () {
      let spaceR = this.$refs['space'].getBoundingClientRect()
      // let widther = this.$refs['widther']
      // widther.style.width = `${spaceR.width * 0.5 + 300 / 2 + 400 * 10}px`
      // widther.style.height = `1px`
      let tl = this.tl = anime.timeline()
      let step1 = {
        targets: this.$refs['itemset']
      }

      tl.add({
        ...step1,
        opacity: 1,
        elasticity: 50,
        translateY: -250 + spaceR.height * -0.2,
        translateX (el, i, n) {
          return (i - 0.5 * n) / n * (n * 50)
        },
        rotateZ (el, i, n) {
          return (i - 0.5 * n) / n * 67
        },
        // rotateY (el, i, n) {
        //   return 15
        // },
        delay (el, i, n) {
          return i * 50
        },
        duration: 1500
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
  font-family: monospace;
  font-size: 100%;
  opacity: 0;
  position: absolute;
  bottom: 0;
  /* left: calc(50% - 300px / 2); */
  /* width: 300px; */
  line-height: 300px;
  text-align: center;
  /* background-color: rgba(255,255,255,0.5); */
  /* border: grey solid 1px; */
  /* padding: 30px; */
}
.center{
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
}
</style>
