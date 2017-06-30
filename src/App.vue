<template>
  <div id="app" class="container">
    <stopwatch :times="times"></stopwatch>
    <div class="row">
      <div class="col-6">
        # Laps: <input type="number" v-model="lapCount" />
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <timetable :cadets="cadets" :lap-count="lapCount" :times="times"></timetable>
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <b-button @click="addCadet">Add Cadet</b-button>
      </div>
    </div>
  </div>
</template>

<script>
import Stopwatch from './components/Stopwatch'
import Timetable from './components/Timetable'

export default {
  name: 'app',
  components: {
    Stopwatch,
    Timetable
  },
  data () {
    return {
      cadets: [],
      lapCount: 0,
      times: [0, 0, 0]
    }
  },
  methods: {
    addCadet: function () {
      const cadet = {
        name: null,
        laps: []
      }
      this.cadets.push(cadet)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
