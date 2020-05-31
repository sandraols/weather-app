<template>
  <section class="second__page">
    <div class="top">
      <!-- <input type="checkbox" v-model="showCurrent"> -->
      <div class="top__header">
        <h2 class="main__title main__title--small">
          How's the
          <br>weather?
          <div class="sun sun--small"></div>
        </h2>
        <input
          v-on:keyup.enter="$emit('getWeather')"
          :value="city"
          v-on:input="$emit('input', $event.target.value)"
          class="input"
          type="text"
          placeholder="How's the weather in..."
        >
      </div>
      <second-page-current-weather v-if="showCurrent" :currentWeather="currentWeather" />
    </div>
    <div class="bottom">
      <div class="bottom__content">
        <div class="column column--bottom">
          <p class="bottom__title">Today</p>

          <p class="bottom__paragraph"></p>
          <img v-bind:src="`http://openweathermap.org/img/wn/` + currentWeather.icon + `@2x.png`"/>
          <!-- <div v-for="item in newArray" :key="item.id">
                            {{item}}
          </div>-->
          <p class="bottom__temperature">temperature</p>
        </div>
        <div class="column column--bottom">
          <p class="bottom__title">Tomorrow</p>
        </div>
        <div class="column column--bottom">
          <p class="bottom__title">Sunday</p>
        </div>
        <div class="column column--bottom">
          <p class="bottom__title">Monday</p>
        </div>
        <div class="column column--bottom">
          <p class="bottom__title">Tuesday</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import SecondPageCurrentWeather from "./SecondPageCurrentWeather.vue";
export default {
  name: "SecondPage",
  props: {
    weather: Object,
    city: String,
  },
  data() {
    return {
      showCurrent: true,
      showHourly: true,
      showDaily: true,
    };
  },
  computed: {
    currentWeather() {
      return {
        city: this.weather.city.name,
        mainWeather: this.weather.list[0].weather[0].main,
        descriptionWeather: this.weather.list[0].weather[0].description,
        temperature: this.weather.list[0].main.temp,
        maxTemp: this.weather.list[0].main.temp_max,
        minTemp: this.weather.list[0].main.temp_min,
        feelsLike: this.weather.list[0].main.feels_like,
        humidity: this.weather.list[0].main.humidity,
        wind: this.weather.list[0].wind.speed,
        icon: this.weather.list[0].weather[0].icon
      }
    }
  },
  components: {
    SecondPageCurrentWeather
  }
};
</script>

<style lang="scss" scoped>
.top {
  height: 50vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: linear-gradient(180deg, #83a5ff 0%, #ffdffc 100%);
}

.top__header {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  width: 80vw;
  height: 14vh;
  margin-bottom: 12px;
}

.main__title--small {
  font-size: 24px;
  font-weight: 300;
}

.sun--small {
  width: 200px;
  height: 200px;
  top: -80px;
  left: 22px;
  background: linear-gradient(
    309.22deg,
    rgba(255, 221, 210, 0.63) 21.58%,
    rgba(255, 160, 160, 0) 67.08%
  );
}

.column {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.bottom {
  display: flex;
  justify-content: center;
  padding: 10px;
}

.bottom__content {
  width: 80vw;
  min-height: 50vh;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.column--bottom {
  // justify-content: space-around;
  height: 80%;
}

.bottom__title {
  font-family: "Roboto", sans-serif;
  color: #3f3f3f;
  font-size: 14px;
}
</style>
