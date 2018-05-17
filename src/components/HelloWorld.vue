<template>
  <div
    id="dia"
      @mousemove="mousemoveApp"
      @mouseup="mouseupApp"
      @touchmove="mousemoveApp"
      @touchend="mouseupApp"
  >
    <svg viewbox="0 0 300 200" width="300" height="200">
      <line :x1="p[0].x + 30" :y1="p[0].y + 20" :x2="p[1].x" :y2="p[1].y" stroke="black"></line>
      <rect :x="p[0].x" :y="p[0].y" width=60 height="40" fill="red" @mousedown="mousedownPoint(1)" @touchstart="mousedownPoint(1)" />
      <circle :cx="p[1].x" :cy="p[1].y" :r="r1" fill="green" @mousedown="mousedownPoint(2)" @touchstart="mousedownPoint(2)"/>
    </svg>
    <div>
      <input type="range" v-model="r1">
    </div>
    <h1>{{ msg }}</h1>
    </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'SVG Dia Study',
      moveIndex: null,
      r1: 30,
      p: [
        {x: 10, y: 10},
        {x: 150, y: 150},
        {x: 60, y: 50},
        {x: 510, y: 10}
      ]
    }
  },
  methods: {
    mousedownPoint (index) {
      this.moveIndex = index
    },
    mousemoveApp (e) {
      if (this.moveIndex) {
        var x = e.pageX
        var y = e.pageY
        if (this.moveIndex === 1) {
          x -= 30
          y -= 20
        }
        this.setPosition(this.moveIndex - 1, x, y)
      }
    },
    mouseupApp (e) {
      if (this.moveIndex) {
        console.log('index: ' + this.moveIndex + ' x: ' + e.pageX + ' y: ' + e.pageY)
        this.moveIndex = null
      }
    },
    setPosition (index, x, y) {
      this.p.splice(index, 1, {
        x: x,
        y: y
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
</style>
