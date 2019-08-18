<template>
  <div>
    <h1>ISS Position</h1>
    <p>{{ stationPosition }}</p>

    <GmapMap
      :center="position"
      :zoom="7"
      map-type-id="terrain"
      class="map-size"
    >
      <GmapMarker
        :position="position"
        :draggable="true"
        :icon="icon"
      />
    </GmapMap>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      stationPosition: null,
      latitude: 0,
      longitude: 0,
      position: {
        lat: 0,
        lng: 0
      },
      icon: {
        url: require('@/assets/iss.png'), // url
        scaledSize: new google.maps.Size(50, 50), // scaled size
        origin: new google.maps.Point(0,0), // origin
        anchor: new google.maps.Point(30, 20) // anchor
      }
    }
  },

  mounted () {
    setInterval(this.getPosition, 1000)
  },

  watch: {
    stationPosition () {
      this.latitude = this.stationPosition.latitude
      this.longitude = this.stationPosition.longitude
      this.position.lat = parseFloat(this.latitude)
      this.position.lng = parseFloat(this.longitude)
    }
  },

  methods: {
    getPosition () {
      axios.get(`http://api.open-notify.org/iss-now.json`)
      .then(response => {
        this.stationPosition = response.data.iss_position
      })
      .catch(e => {
        console.log(e);
      })
    }
  }
}
</script>

<style>
.map-size {
  width: auto;
  height: 50vh;
  margin: 0 10vw;
}
</style>
