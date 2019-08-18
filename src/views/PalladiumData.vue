<template>
  <div>
    <h1>Palladium course</h1>
    <chart :chart-data="palladiumPrices"></chart>
  </div>
</template>

<script>
import axios from 'axios'
import Chart from "@/chart.js";

export default {
  components: {
    Chart
  },

  data () {
    return {
      palladiumPrices: null
    }
  },

  mounted () {
    axios.get(`https://www.quandl.com/api/v3/datasets/LPPM/PALL.json?api_key=${process.env.VUE_APP_QUANDL}`)
    .then(response => {
      return response.data.dataset.data.reverse()
    })
    .then(palladiumData => {
      this.palladiumPrices = {
        labels: palladiumData.slice(palladiumData.length/2, palladiumData.length).filter((item, index) => index % 2).map(i => i[0]),
        datasets: [
          {
            label: "Palladium",
            backgroundColor: "rgba(153, 102, 255, 0.5)",
            data: palladiumData.slice(palladiumData.length/2, palladiumData.length).filter((item, index) => index % 2).map(i => i[2])
          }
        ]
      }
    })
    .catch(e => {
      console.log(e);
    })
  }
}
</script>

<style>
</style>
