<template>
  <div>
    <h1>Hello data</h1>
    <button @click="getData">Get token</button>
    <p>{{ token }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      token: 'Pas encore de token',
      palladiumPrices: null
    }
  },

  mounted () {
    axios.get(`https://www.quandl.com/api/v3/datasets/LPPM/PALL.json?api_key=${process.env.VUE_APP_QUANDL}`)
    .then(response => {
      this.palladiumPrices = response.data.dataset.data
    })
    .catch(e => {
      console.log(e);
    })
  },

  methods: {
    getData () {
      this.token = "Tu m'as cliqué"

      axios.get(`https://api.myjson.com/bins/6muxh`)
      .then(response => {
        // JSON responses are automatically parsed.
        this.mockData = response.data
      })
      .catch(e => {
        console.log(e);
      })

      // const config = {
      //  headers: {'Authorization': authString}
      // }
      //
      // const request = axios.get(
      // `https://api.helloworks.com/v3/token/${publicKey}`,
      // config)
      // .then((result) => {
      //   console.log('result', result);
      // })
      // .catch(err => {
      //   console.log(err);
      // })
    }
  }
}
</script>

<style>
</style>
