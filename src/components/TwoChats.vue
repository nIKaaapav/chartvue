<script>
import { Bar } from 'vue-chartjs'

export default {
  name: "TwoChart",
  extends: Bar,
  props: {
    dataBar: {
      type: Array,
      default: null
    },
    dataLine: {
      type: Array,
      default: null
    },
    labels: {
      type: Array,
      default: null
    },
  },
  data(){
    return {
      chartdata: {
      labels: this.labels[0],
          datasets: [
      {
        type: 'bar',
        label: 'Countries',
        data: this.dataBar,
        color: '#f87979',
      },
      {
        type: 'line',
        label: 'Daths',
        data: this.dataLine,
        color: '#7979f8',
      }
    ]
      },
    }
  },
  mounted () {
    this.renderChart(this.chartdata)
  }
}
</script>

<style scoped>

</style>