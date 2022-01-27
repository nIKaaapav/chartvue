<script>
import { Bar } from 'vue-chartjs'

export default {
  name: "ChartBar",
  extends: Bar,
  props: {
    data: {
      type: Array,
      default: null
    },
    labels: {
      type: Array,
      default: null
    },
  },
  data(){
    return  {
      chartdata: {
        labels: this.labels[0],
        datasets: [
          {
            label: 'Countries',
            backgroundColor: '#f87979',
            data: this.data
          }
        ]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false
      }
    }
  },
  mounted () {
    this.renderChart(this.chartdata)
  }
}
</script>

<style scoped>

</style>