<template lang="pug">
.main
  show-station(
    :stations="stations"
    :random-index="randomIndex"
  )
  custom-button(
    v-show="status === 'wait'"
    text="start"
    @on-click="rouletteStart"
  )
  custom-button(
    v-show="status === 'run'"
    text="stop"
    @on-click="rouletteStop"
  )
</template>

<script>
import Stations from '@/composables/data/stations'
import ShowStation from '@/components/layouts/ShowStation'
import CustomButton from '@/components/forms/CustomButton'

export default {
  name: 'App',

  components: {
    ShowStation,
    CustomButton
  },

  data() {
    return {
      // 路線
      lines: [],
      stations: [],
      randomIndex: -1,
      // wait or run
      status: 'wait'
    }
  },

  created() {
    this.getAllStations()
    this.setStations()
  },

  methods: {
    /**
     * 登録されている全ての駅を取ってくる
     */
    getAllStations() {
      const { yamanoteLine } = Stations()
      this.lines.push(yamanoteLine)
    },
    /**
     * 駅名だけを取り出した配列を作る
     */
    setStations() {
      this.lines.forEach((line) => {
        this.stations = this.stations.concat(line.stations)
      })
    },
    /**
     * ランダムでindexを取得
     */
    getRandom() {
      this.randomIndex = Math.floor(Math.random() * this.stations.length)
    },
    /**
     * スタートボタンクリック
     */
    rouletteStart() {
      this.status = 'run'
      let random = setInterval(() => {
        this.getRandom()
        if (this.status === 'wait') {
          clearInterval(random)
        }
      }, 100)
    },
    /**
     * ストップボタンクリック
     */
    rouletteStop() {
      this.status = 'wait'
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
