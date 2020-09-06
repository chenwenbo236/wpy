<template>
  <div class="map">
    <div style="width:100%;height: 400px" ref="mapchart">echart</div>
    <div style="width:100%;height: 400px" ref="mapchart">echart</div>
    <div style="width:100%;height: 400px" ref="mapchart">echart</div>
  </div>
</template>

<script>
import echarts from 'echarts'
import 'echarts/map/js/china.js';

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
      echart: null
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
      this.option = this.chartData
      if (this.echart) {
        this.echart.setOption(this.option)
      } else {
        this.echart = echarts.init(this.$refs.mapchart)
        this.echart.setOption(this.option)
      }
      this.echart.on('click', this.mapShow)
    },
    mapShow(params) {
      alert(params.name)
    }
  },
  beforeDestroy() {
    this.echart.off('click', this.mapShow)
  }
}
</script>

<style lang='scss' scoped>
</style>
