<template>
  <div class="no_display">
    
  </div>
</template>

<script>
const axios = require('axios').default;
const ipRegex = /ip=(\d{1,3}.\d{1,3}.\d{1,3}.\d{1,3})$/gmi
export default {
  name: 'ip',
  props:{
      ip: String,
      country: String,
      City: String,
      lat: Number,
      long: Number
  },
  mounted () {
    axios.get('https://www.cloudflare.com/cdn-cgi/trace')
    .then(response => (
        this.ip = ipRegex.exec(response.data)[1]
    )
        .then(
            axios.get('https://cors-anywhere.herokuapp.com/http://api.ipstack.com/'+this.ip+'?access_key=<key>')
            .then( response => (
                    this.lat = response.data.latitude,
                    this.long = response.data.longitude,
                    this.country = response.data.country_name,
                    this.city = response.data.city
                ).then(
                    this.$emit('response', {
                        ip: this.ip,
                        lat: this.lat,
                        long: this.long,
                        country: this.country,
                        city: this.city
                    })
                )
            )
        )
    )
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
