<template>
  <table class="table table-sm table-bordered table-striped">
    <thead>
      <tr>
        <th>&nbsp;</th>
        <th>Name</th>
        <th v-for="(lap, idx) in laps">Lap {{idx + 1}}</th>
      </tr>
    </thead>
    <tbody>
      <tr scope="row" v-for="cadet in cadets" :class="{'table-success': cadet.laps.length >= laps.length}">
        <th>
          <b-button variant="primary" @click="lapCadet(cadet)" :disabled="cadet.laps.length >= laps.length">
            <icon name="clock-o"></icon>
          </b-button>
          <b-button variant="danger" @click="clearLaps(cadet)">
            <icon name="eraser"></icon>
          </b-button>
          <b-button variant="danger" @click="$emit('removeCadet', cadet)">
            <icon name="trash-o"></icon>
          </b-button>
        </th>
        <td>
          <input v-model="cadet.name" placeholder="Curry" />
        </td>
        <td v-for="(lap, idx) in laps">
          <span v-if="cadet.laps[idx]">
            {{cadet.laps[idx]}}
          </span>
          <span v-if="!cadet.laps[idx]" class="text-muted">
            <small><em>N/A</em></small>
          </span>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import 'vue-awesome/icons/clock-o'
import 'vue-awesome/icons/trash-o'
import 'vue-awesome/icons/eraser'

function pad0 (value, count) {
  let out = value.toString()
  for (; out.length < count; --count) {
    out = '0' + out
  }
  return out
}

export default {
  name: 'timetable',
  props: ['lapCount', 'cadets', 'times'],
  data () {
    return {
      laps: []
    }
  },
  watch: {
    lapCount: function (count) {
      this.setupLaps(count)
    }
  },
  methods: {
    lapCadet: function (cadet) {
      cadet.laps.push(`${pad0(this.times[0], 2)}:${pad0(this.times[1], 2)}`)
    },
    clearLaps: function (cadet) {
      cadet.laps = []
    },
    setupLaps: function (count) {
      var newlaps = []
      newlaps.length = count
      this.laps = newlaps
    }
  },
  beforeMount: function () {
    this.setupLaps(this.lapCount)
  }
}
</script>

<style scoped>
table {
  width: 100%;
}
</style>
