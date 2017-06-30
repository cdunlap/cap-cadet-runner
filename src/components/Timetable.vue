<template>
  <table>
    <thead>
      <tr>
        <th>&nbsp;</th>
        <th>Name</th>
        <template v-for="(lap, idx) in laps">
          <th>Lap {{idx + 1}}</th>
        </template>
      </tr>
    </thead>
    <tbody v-for="cadet in cadets">
      <tr>
        <td>
          <b-button size="sm" variant="primary" @click="lapCadet(cadet)">
            <icon name="clock-o"></icon>
          </b-button>
        </td>
        <td>
          <input v-model="cadet.name" placeholder="Curry" />
        </td>
        <template v-for="(lap, idx) in laps">
          <td>{{cadet.laps[idx]}}</td>
        </template>
      </tr>
    </tbody>
  </table>
</template>

<script>
import 'vue-awesome/icons/clock-o'

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
      var newlaps = []
      newlaps.length = count
      this.laps = newlaps
    }
  },
  methods: {
    lapCadet: function (cadet) {
      cadet.laps.push(`${pad0(this.times[0], 2)}:${pad0(this.times[1], 2)}`)
    }
  }
}
</script>

<style scoped>
table {
  width: 100%;
}
</style>
