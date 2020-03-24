<template>
  <div class="Hi">
    <h1>{{msg}} {{city}}, {{country}}</h1>
    <h2>Temp: {{ temp }}f</h2>
    <h2>Conditions: {{ conditions }}</h2>
  </div>
</template>

<script>

const axios = require('axios').default;
export default {
  name: 'Weather',
  props: {
    msg: String,
    resp: String,
    ip: String,
    lat: Number,
    long: Number,
    city: String,
    country: String,
    temp: String,
    conditions: String
  },
  mounted () {
    axios
      .get('https://cors-anywhere.herokuapp.com/https://api.darksky.net/forecast/<key>/'+this.lat+','+this.long)
      .then(response => (
        this.resp = response.data,
        this.temp = response.data.currently.temperature,
        this.conditions = response.data.currently.summary
      ))
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
