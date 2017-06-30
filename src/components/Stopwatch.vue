<template>
  <div class="row">
    <div class="col-10 time">
      <b-card class="well"><h1>{{displayTime}}</h1></b-card>
    </div>
    <div class="col-2 actions">
      <b-button-group>
        <b-button v-if="!running" @click="start" size="lg" variant="success">
          <icon name="play"></icon>
        </b-button>
        <b-button v-if="running" @click="pause" size="lg" variant="danger">
          <icon name="pause"></icon>
        </b-button>
        <b-button @click="reset" size="lg" variant="primary">
          <icon name="refresh"></icon>
        </b-button>
      </b-button-group>
    </div>
  </div>
</template>

<script>
import 'vue-awesome/icons/play'
import 'vue-awesome/icons/pause'
import 'vue-awesome/icons/stop'
import 'vue-awesome/icons/refresh'

function pad0 (value, count) {
  let out = value.toString()
  for (; out.length < count; --count) {
    out = '0' + out
  }
  return out
}

export default {
  name: 'stopwatch',
  props: ['times'],
  data () {
    return {
      time: null,
      // times: [0, 0, 0],
      displayTime: '',
      running: false,
      paused: false
    }
  },
  methods: {
    start: function () {
      if (!this.time) {
        this.time = performance.now()
      }
      if (!this.running) {
        this.running = true
        requestAnimationFrame(this.step)
      }
    },

    pause: function () {
      this.running = false
      this.time = null
    },

    reset: function () {
      this.running = false
      this.time = null
      this.times = [0, 0, 0]
      this.display()
    },

    step: function (timestamp) {
      if (!this.running) return
      this.calculate(timestamp)
      this.time = timestamp
      this.display()
      requestAnimationFrame(this.step)
    },

    display: function () {
      this.displayTime = `${pad0(this.times[0], 2)}:${pad0(this.times[1], 2)}:${pad0(Math.floor(this.times[2]), 2)}`
    },

    calculate: function (timestamp) {
      // This function has the component bound to it, why is `this.times` undefined?!
      const diff = timestamp - this.time
      this.times[2] += diff / 10
      if (this.times[2] >= 100) {
        this.times[1] += 1
        this.times[2] -= 100
      }

      if (this.times[1] >= 60) {
        this.times[0] += 1
        this.times[1] -= 60
      }
    }
  },

  beforeMount: function () {
    this.display()
  }
}
</script>

<style scoped>
</style>
