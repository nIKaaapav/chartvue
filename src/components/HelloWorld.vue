<template>
  <div>
    <button v-on:click="fetch">Click</button>
    <Chart :labels='[this.labelsLine]' :data="this.dataLine" v-if="isOpen"/>
    <ChartBar :labels='[this.labelsBar]' :data="this.dataBar" v-if="isOpen"/>
    <TwoChart :labels='[this.labelsLine]' :dataBar="this.dataBar" :dataLine="this.dataLine" v-if="isOpen"/>

  </div>
</template>

<script>
import Chart from "@/components/Chart";
import ChartBar from "@/components/ChartBar";
import TwoChart from "@/components/TwoChats";
import Papa from 'papaparse';

export default {
  name: 'HelloWorld',
  components: {Chart, ChartBar, TwoChart},
  data() {
    return {
      dataChart: [],
      labelsLine: [],
      labelsBar: [],
      dataBar: [],
      dataLine: [],
      isOpen: false,
    }
  },
  methods: {
    fetch() {
      fetch("COVID.csv").then(
          res =>
            res.text()
      ).then(res => {
        const arr = []
        const results = Papa.parse(res, {delimiter: ","}).data;
        const headers = results[0];
        for (let  i = 1; i< results.length; i++){
          let obj = {}
          for (let j = 0; j < headers.length; j++) {
            obj[headers[j]] = results[i][j]
          }
          arr.push(obj);
        }
        this.dataChart = arr;
        this.isOpen = true;

        this.labelsLine = this.dataChart.map(x => x.dateRep);
        this.dataLine = this.dataChart.map(x => +x.deaths);

        this.labelsBar =  this.dataChart.map(x => x.countriesAndTerritories);
        this.dataBar =  this.dataChart.map(x => +x.popData2020);
        return arr;
      })
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
