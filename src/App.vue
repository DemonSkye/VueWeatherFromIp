<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <ip @response="onResponse" />
    <Weather v-if="responseReady" msg="The weather for:" :lat="lat" :long="long" :ip="ip" :city="city" :country="country"/>
  </div>
</template>

<script>
import Weather from './components/Weather.vue'
import ip from './components/Ip_resolve.vue'

export default {
  name: 'App',
  data() {
    return {
      lat: 0,
      long: 0,
      ip: 0,
      country: 0,
      city: 0,
      responseReady: false
    }
  },
  components: {
    Weather,
    ip
  },
  methods: {
    onResponse(event) {
      this.lat = event.lat
      this.long = event.long
      this.ip = event.ip
      this.country = event.country
      this.city = event.city
      this.responseReady = true;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
