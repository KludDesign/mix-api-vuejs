<template>
  <chart :chart-data="datacollection"></chart>
</template>

<script>
import Chart from "@/chart.js";

export default {
  components: {
    Chart
  },
  data() {
    return {
      datacollection: null
    }
  },
  mounted() {
    this.fillData()
  },
  methods: {
    fillData() {
      this.datacollection = {
        labels: [
          "January",
          "February",
          "March",
          "April",
          "May",
          "June",
          "July",
          "August",
          "September",
          "October",
          "November",
          "December"
        ],
        datasets: [
          {
            label: "Fibonacci",
            backgroundColor: "rgba(153, 102, 255, 0.5)",
            data: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
          },
          {
            label: "GitHub Commits",
            backgroundColor: "#f87979",
            data: [70, 20, 12, 39, 100, 40, 95, 80, 80, 20, 12, 101]
          },
          {
            label: "Monthly incomes",
            backgroundColor: "#A5CC82",
            data: [205, 408, 188, 190, 58, 200, 190, 400, 164, 254, 290, 201]
          }
        ]
      }
    }
  }
}
</script>

<style>
</style>
