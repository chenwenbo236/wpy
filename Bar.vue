<template>
  <div class="bar">
    <div style="width:100%;height: 400px" ref="mapchart">echart</div>
  </div>
</template>

<script>
import echarts from 'echarts'

export default {
  props: {
    chartData: {
      type: Object,
      default() {
        return {
        }
      }
    }
  },
  data() {
    return {
      echart: null,
      width: 11
    }
  },
  watch: {
    chartData: {
      handler() {
        this.initChart()
      },
      deep: true
    }
  },
  mounted() {
    this.initChart()
  },
  methods: {
    initChart() {
      if (this.echart) {
        this.echart.setOption(this.chartData)
      } else {
        this.echart = echarts.init(this.$refs.mapchart)
        this.echart.setOption(this.chartData)
      }
      this.echart.on('click', this.mapShow)
    },
    mapShow(params) {
      this.$router.push({
        path: '/projectDetail?name=' + params.name
      })
    }
  }
}
</script>

<style lang='scss' scoped>
</style>
