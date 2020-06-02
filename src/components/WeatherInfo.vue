<template>
  <div class="weather-info-container">
    <p class="text time">{{time | subStr}}</p>
    <img class="icon" v-bind:src="`http://openweathermap.org/img/wn/` + icon + `@2x.png`">
    <p class="text">{{Math.round(temperature)}}˚C</p>
  </div>
</template>

<script>
export default {
  name: "WeatherInfo",
  props: {
    time: String,
    icon: String,
    temperature: Number
  },
  filters: {
    subStr: function(string) {
      return string.substring(16, 11);
    }
  }
};
</script>

<style lang="scss" scoped>
.weather-info-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 10vw;
  height: fit-content;
  padding: 10px;
}
.text {
  font-family: "Roboto", sans-serif;
  color: #3f3f3f;
  font-size: 14px;
}
.time {
    font-weight: 700;
}
.icon {
  max-width: 60px;
}
@media screen and (max-width: 414px) {
  .weather-info-container {
    width: fit-content;
  }
  .time {
    margin-top: 24px;
  }
}
</style>
