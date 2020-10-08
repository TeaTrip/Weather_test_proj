<template>
  <div class="col-sm">
      <b-card bg-variant="secondary" text-variant="white" class="text-center">
        <b-card-text>{{day[offset]}}</b-card-text>
        <hr>
        <div class="row">
          <div class="col">
            <img v-bind:src="weathericon" alt="">
          </div>
          <div class="col" id="temperature">
            {{Math.round(weather.daily[offset].temp.max)}}℃
          </div>
        </div>
      </b-card>
  </div>
</template>

<script>

export default {
  props: ['weather','offset','day','weathericon'],
  name: "WeatherCard",
}

</script>

<style scoped>

#temperature{
  color: #FFF;
  font-size: 102px;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>