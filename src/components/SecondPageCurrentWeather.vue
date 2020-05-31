<template>
  <div class="top__content">
    <h2 class="title__city">{{currentWeather.city}}</h2>
    <div class="weather__info">
      <div class="column">
        <p
          class="main__weather">{{currentWeather.mainWeather}} - {{currentWeather.descriptionWeather}}</p>
        <p class="temperature">{{Math.round(currentWeather.temperature)}}˚C</p>
      </div>
      <div class="column">
        <p class="weather__paragraph">Feels like: {{Math.round(currentWeather.feelsLike)}}˚C</p>
        <p class="weather__paragraph">Max temp: {{Math.round(currentWeather.maxTemp)}}˚C</p>
        <p class="weather__paragraph">Min temp: {{Math.round(currentWeather.minTemp)}}˚C</p>
      </div>
      <div class="column">
        <p class="weather__paragraph">Humidity: {{currentWeather.humidity}}%</p>
        <p class="weather__paragraph">Wind: {{Math.round(currentWeather.wind)}} m/s</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SecondPageCurrentWeather",
  props: {
    currentWeather: Object
  }
};
</script>

<style lang="scss" scoped>
.top__content {
  width: 80vw;
  margin-top: 50px;
}

.title__city {
  font-family: "Rubik", sans-serif;
  font-size: 48px;
  color: white;
  margin-bottom: 20px;
}

.weather__info {
  height: 74px;
  width: 70vw;
  display: flex;
  justify-content: space-between;
}

.column {
  display: flex;
  flex-direction: column;
}

.main__weather {
  font-family: "Roboto", sans-serif;
  font-size: 18px;
  color: white;
  margin-bottom: 14px;
}

.description__weather {
  font-family: "Roboto", sans-serif;
  font-size: 14px;
  color: white;
}

.temperature {
  font-family: "Roboto", sans-serif;
  font-size: 18px;
  color: white;
}

.weather__paragraph {
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  color: white;
  margin-bottom: 8px;
}
</style>
