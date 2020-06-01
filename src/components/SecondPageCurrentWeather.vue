<template>
  <div class="top__content">
    <h2 class="title__city">{{currentWeather.city}}</h2>
    <div class="weather__info">
      <div class="column">
        <p
          class="main__weather">{{currentWeather.mainWeather}} <br><span class="description__weather">{{currentWeather.descriptionWeather}}</span></p>
        <p class="temperature">{{Math.round(currentWeather.temperature)}}˚C</p>
      </div>
      <div class="weather__info--columns">
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
  margin-top: 70px;
}

.title__city {
  font-family: "Rubik", sans-serif;
  font-size: 56px;
  color: white;
  margin-bottom: 20px;
}

.weather__info {
  height: 74px;
  width: fit-content;
  display: flex;
  // flex-direction: column;
  justify-content: space-between;
}

.column {
  display: flex;
  flex-direction: column;
  margin-right: 12vw;
}
// .weather__info--columns .column:nth-of-type(1) {
//   margin-right: 10vw;
// }
.column:last-of-type {
  margin-right: 0;
}
.weather__info--columns {
  width: 40vw;
  display: flex;
  // justify-content: space-between;
}
.main__weather {
  font-family: "Roboto", sans-serif;
  font-size: 22px;
  color: white;
  margin-bottom: 14px;
}
.description__weather {
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  color: white;
}
.temperature {
  font-family: "Roboto", sans-serif;
  font-size: 22px;
  color: white;
}
.weather__paragraph {
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  color: white;
  margin-bottom: 8px;
}
@media screen and (max-width: 590px) {
  .top__content {
    margin-top: 20vh;
  }
  .weather__info {
    flex-direction: column;
  }
  .weather__paragraph {
    width: 25vw;
  }
  .column {
    flex-direction: row;
  }
  .column:nth-of-type(2) {
    flex-direction: column;
  }
  .weather__info--columns .column:nth-of-type(1) {
  flex-direction: column;
  }
  .weather__info--columns {
    display: flex;
    flex-direction: row;
  }
  .main__weather {
    margin-right: 24px;
    margin-bottom: 38px;
  }
}
</style>
