<template>
  <div class="weather-page">
    <div class="weather-detail" v-if="weather.temp">

      <img class="weather-img" :src="`https://www.weatherbit.io/static/img/icons/${weather.weather?.icon ? weather.weather.icon : 'r01d' }.png`" :alt=weather.weather?.description />
      <p class="weather">{{weather.weather?.description}},</p>
      <p>{{convertTemp(weather.temp)}}°</p>
    </div>
    <div v-else></div>
    <div class="weather-search">
      <fa icon="fa-solid fa-magnifying-glass" />
    </div>

  </div>
</template>

<script>
  import axios from 'axios'
export default {
  name: 'Weather',
  data(){
    return {
      weather: {},
      locCoordinate: {lat: '', lon: ''},
    }
  },
  mounted(){
    this.getLocation()
  },
  watch:{
    locCoordinate:{
      handler(){

        this.getCurWeather()
      },
      deep: true
    },
  },
  methods:{
    async getCurWeather(){

      const res = await axios.get(`https://weatherbit-v1-mashape.p.rapidapi.com/current`, {params:{lon: this.locCoordinate.lon, lat: this.locCoordinate.lat}, headers: {
            'X-RapidAPI-Key': '93ca3a18dbmshe726aeae2cb1c33p1ec27ajsn9fc9e9dc0389',
            'X-RapidAPI-Host': 'weatherbit-v1-mashape.p.rapidapi.com'
        }})
      this.weather = res.data.data[0]
    },
    getLocation(){
      if(navigator.geolocation){
        navigator.geolocation.getCurrentPosition(this.setLocCoords)
      }else{
        console.log('can\' get location')
      }
  
    },
    setLocCoords(position){
      this.locCoordinate.lat = position.coords.latitude
      this.locCoordinate.lon = position.coords.longitude
    },
    convertTemp(temp){
      return (temp * (9/5) +32).toFixed(1)
    }

  }
}
</script>

<style>
.weather{
  margin: 0 3px;
}
.weather-page {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.weather-detail{
  display: flex;
  justify-content: center;
  align-items: center;
  
  width: fit-content;
  padding: 4px 8px;
  background-color: #ccc;
  border-radius: 50px;

  font-size: 12px;
}
.weather-img {
  width: 20px;

}
</style>