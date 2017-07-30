<template>
  <div id="app" class="container-fluid">
    <stopwatch :times="times"></stopwatch>
    <div class="row">
      <div class="col-6">
        <!-- <strong># Laps:</strong> <input type="number" v-model="lapCount" /> -->
        <b-form-fieldset label="# of Laps" :horizontal="true">
          <b-form-input v-model="lapCount" type="number" min="1"></b-form-input>
        </b-form-fieldset>
      </div>
      <div class="col-6">
        <b-button @click="addCadet" variant="success">Add Cadet</b-button>
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <timetable :cadets="cadets" :lap-count="lapCount" :times="times" @removeCadet="removeCadet"></timetable>
      </div>
    </div>
    <footer>
      <p class="text-muted"><small>v 1.0.1 (7/30/2017) &middot; <a href="https://github.com/cdunlap/cap-cadet-runner" target="_blank">View Source and Guide On <icon name='github'></icon></a></small></p>
    </footer>
  </div>
</template>

<script>
import Stopwatch from './components/Stopwatch'
import Timetable from './components/Timetable'
import 'vue-awesome/icons/github'

export default {
  name: 'app',
  components: {
    Stopwatch,
    Timetable
  },
  data () {
    return {
      cadets: [],
      lapCount: 1,
      times: [0, 0, 0]
    }
  },
  methods: {
    addCadet: function () {
      const cadet = {
        id: this.cadets.length,
        name: null,
        laps: []
      }
      this.cadets.push(cadet)
    },
    removeCadet: function (cadet) {
      const idx = this.cadets.findIndex(c => c.id === cadet.id)
      if (idx !== -1) {
        this.cadets.splice(idx, 1)
      }
    }
  }
}
</script>
