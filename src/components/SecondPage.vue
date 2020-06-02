<template>
  <section class="second__page">
    <div ref="topDiv" class="top" v-bind:class="backgroundClass">
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
      <second-page-current-weather :currentWeather="currentWeather"/>
    </div>
    <div class="bottom">
      <div class="bottom__content">
        <div
          class="column"
          v-bind:key="dayObject.date"
          v-for="dayObject in forecasts"
        >
          <h2 class="bottom__title">{{getDay(dayObject.date)}}</h2>
          <div class="weather__info">
            <template v-for="weather in dayObject.hourlyForecasts">
              <weather-info
                v-bind:key="weather.dt_txt"
                :time="weather.dt_txt"
                :icon="weather.weather[0].icon"
                :temperature="weather.main.temp"
              />
            </template>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import SecondPageCurrentWeather from "./SecondPageCurrentWeather.vue";
import WeatherInfo from "./WeatherInfo.vue";
export default {
  name: "SecondPage",
  props: {
    weather: Object,
    city: String
  },
  computed: {
    nameLength(){
      return this.name.length;
    },
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
        icon: this.weather.list[0].weather[0].icon,
        showTime: this.weather.list[0].dt_txt
      };
    },
    forecasts() {
      let forecasts = [];
      // All data from weather.list in a new shallow copy
      const allHourlyForecasts = Array.from(this.weather.list);
      // the index of where tomorrow starts
      const indexOfTomorrow = allHourlyForecasts.findIndex(
        hourlyForecast =>
          hourlyForecast.dt_txt.substring(0, 10) !==
          allHourlyForecasts[0].dt_txt.substring(0, 10)
      );
      // All data from weather.list from index 0 to index of tomorrow = todays forecast

      // loop five times, one for each day
      for (let i = 0; i < 5; i++) {
        if (i === 0) {
          // if first day, date is today and hours are based of indexOfTmorrow
          const hourlyForecasts = allHourlyForecasts.splice(0, indexOfTomorrow);
          if (hourlyForecasts.length > 1) {
            forecasts.push({
              date: "Today",
              hourlyForecasts: hourlyForecasts
            });
          }
        } else {
          forecasts.push({
            date: new Date(allHourlyForecasts[0].dt_txt).getDay(),
            hourlyForecasts: allHourlyForecasts.splice(0, 8)
          });
        }
      }
      return forecasts;
    },
    backgroundClass() {
      switch (this.currentWeather.mainWeather) {
        case "Clear":
          return "clear-sky"
        case "Clouds":
          return "clouds"
        case "Rain":
          return "rain"
        case "Thunderstorm":
          return 'thunderstorm'
        case "Snow":
          return 'snow'
        case "Mist":
          return 'mist'
        default:
          return 'clear-sky'
      }
    },
  },
  methods: {
    getDay(d) {
      if (d === "Today") {
        return "Today";
      }
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday"
      ];
      let day = days[d];
      return day;
    },
  },
  components: {
    SecondPageCurrentWeather,
    WeatherInfo
  },
  filters: {
    subStr: function(string) {
      return string.substring(16, 11);
    }
  }
};
</script>

<style lang="scss" scoped>
.top {
  height: 70vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: linear-gradient(180deg, #83a5ff 0%, #ffdffc 100%);
  overflow: hidden;
}
.clear-sky {
  background: linear-gradient(180deg, #83a5ff 0%, #ffdffc 100%);
}
.clouds {
  background: linear-gradient(180deg, #a3b4de 0%, #e8b9e1 100%);
}
.rain {
  background: linear-gradient(180deg, #35383f 0%, #d9e1ea 100%);
}
.thunderstorm {
  background: linear-gradient(180deg, #402450 0%, #65707d 100%);
}
.snow {
    background: linear-gradient(180deg, #a9ccff 0%, #b4deff 100%);
}
.mist {
 background: linear-gradient(180deg, #b7b7b7 0%, #bfcddd 100%);
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
.bottom {
  display: flex;
  justify-content: center;
  margin-top: 50px;
}
.bottom__content {
  width: 80vw;
  min-height: 50vh;
  padding: 20px 0;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: space-between;
}
.column {
  display: flex;
  flex-direction: column;
  margin-bottom: 4vh;
  padding-bottom: 16px;
  border-bottom: 2px solid #3f3f3f;
}
.bottom__title {
  font-family: "Roboto", sans-serif;
  color: #3f3f3f;
  font-size: 18px;
  margin-bottom: 14px;
  padding-bottom: 8px;
  width: fit-content;
}
.weather__info {
  display: flex;
  margin-left: -3.5vw;
}
@media screen and (max-width: 590px) {
  .top {
    height: 100vh;
  }
  .top__header {
    flex-direction: column;
    padding-top: 24px;
    height: 30vh;
    position: relative;
    z-index: 1;
  }
  .bottom__content {
    flex-direction: column;
  }
  .column {
    flex-direction: column;
    align-items: flex-start;
  }
  .weather__info {
    margin-left: -12px;
    flex-wrap: wrap;
  }
  .bottom__title {
    margin-bottom: 8px;
  }
}
@media screen and (max-width: 414px) {
  .weather__info {
    flex-wrap: wrap;
  }
}
@media only screen and (min-device-width: 414px) and (max-device-width: 736px) {
  .top__header {
    height: 23vh;
  }
}
</style>
