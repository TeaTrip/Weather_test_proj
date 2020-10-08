<template>
  <div id="app">
      <div class="container">
      <h1>Погода в Ростове-на-Дону</h1>
      <hr>
      <div class="row">
        <div class="col-sm">
          <WeatherCard
              v-bind:weather="weather"
              v-bind:weathericon="weathericon1"
              v-bind:day="day"
              v-bind:offset=0
          />
        </div>
        <div class="col-sm">
          <WeatherCard
              v-bind:weather="weather"
              v-bind:weathericon="weathericon2"
              v-bind:day="day"
              v-bind:offset=1
          />
        </div>
        <div class="col-sm">
          <WeatherCard
              v-bind:weather="weather"
              v-bind:weathericon="weathericon2"
              v-bind:day="day"
              v-bind:offset=2
          />
        </div>
      </div>
      </div>
    </div>

</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
import WeatherCard from "@/components/WeatherCard"

function getDateStr(offset){
  let date = new Date(new Date().getTime() + offset*(24 * 60 * 60 * 1000))
  let days = ['Воскресенье', 'Понедельник', 'Вторник', 'Среда', 'Четверг', 'Пятница', 'Суббота']
  var dateInNumberFormat = date.toLocaleDateString()
  return days[date.getDay()] + ' ' + dateInNumberFormat
}

function createIconLink(weather,offset){
  return `http://openweathermap.org/img/wn/${weather.daily[offset].weather[0].icon}@2x.png`
}

export default {
  name: 'App',
  components: {
    WeatherCard
  },
  data (){
    return {
      api_key: '46a60add2b30b7f5bc3a522ec5704ca1',
      url_base: 'http://api.openweathermap.org/data/2.5/',
      lat: '47.2313500',
      lon: '39.7232800',
      weathericon1: '',
      weathericon2: '',
      weathericon3: '',
      day: [
        getDateStr(0),
        getDateStr(1),
        getDateStr(2)],
      weather: {}
    }
  },
  mounted (){
    fetch(`${this.url_base}onecall?lat=${this.lat}&lon=${this.lon}&exclude=current,minutely,hourly,alerts&units=metric&lang=ru&APPID=${this.api_key}`)
        .then(res => res.json())
        .then(json => {
          this.weather = json
          this.weathericon1 = createIconLink(this.weather,0)
          this.weathericon2 = createIconLink(this.weather,1)
          this.weathericon3 = createIconLink(this.weather,2)
        })
  },
  methods: {

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
