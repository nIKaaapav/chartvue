<script>
import { Line } from 'vue-chartjs'

export default {
  name: "Chart",
  extends: Line,
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
           label: 'Daths',
           backgroundColor: '#f87979',
           data: this.data
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