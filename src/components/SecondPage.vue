<template>
  <section class="second__page">
    <div
      ref="topDiv"
      class="top"
    >
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
      <second-page-current-weather v-if="showCurrent" :currentWeather="currentWeather"/>

    </div>
    <div class="bottom">
      <div class="bottom__content">
        <div class="column" v-bind:key="dayObject.date" v-for="dayObject in forecasts">
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
// import axios from 'axios';
import SecondPageCurrentWeather from "./SecondPageCurrentWeather.vue";
import WeatherInfo from "./WeatherInfo.vue"
export default {
  name: "SecondPage",
  props: {
    weather: Object,
    city: String
  },
  data() {
    return {
      showCurrent: true,
      showHourly: true,
      showDaily: true
    };
  },
  computed: {
    currentWeather() {
      // axios
      // .get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=61b1bca9c0906f64bf48a4bf1c04e906`)
      // .then(response => {
      //   this.weather = response.data;
      //   this.gotWeather = true;
      //   this.city = '';
      //   console.log(this.response.data);
      // })
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
        showTime: this.weather.list[0].dt_txt,
      };
    },
    forecasts() {
      let forecasts = [];
      const allHourlyForecasts = this.weather.list; // All data from weather.list
      const indexOfTomorrow = allHourlyForecasts.findIndex(hourlyForecast => hourlyForecast.dt_txt.substring(0, 10) !== allHourlyForecasts[0].dt_txt.substring(0, 10)); // the index where tomorrow starts
       // All data from weather.list from index 0 to index of tomorrow = todays forecast
      
      // loop five times, one for each day
      for (let i = 0; i < 5; i++) {
        if (i === 0) { //if first day, date is today and hours are based of indexOfTmorrow
          forecasts.push({
            date: 'Today',
            hourlyForecasts: allHourlyForecasts.splice(0, indexOfTomorrow)
          })
        } else {
          forecasts.push({
            date: new Date(allHourlyForecasts[0].dt_txt).getDay(),
            hourlyForecasts: allHourlyForecasts.splice(0, 8)
          })
        }
      }
      return forecasts;
    }
  },
  methods: {
    getDay(d) {
        if (d === 'Today') {
          return 'Today'
        }
        let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
        let day = days[d];
        return day;
    }
  },
  components: {
    SecondPageCurrentWeather,
    WeatherInfo,
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
  height: 60vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: linear-gradient(180deg, #83a5ff 0%, #ffdffc 100%);
  overflow: hidden;
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
  // padding: 10px;
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
  // align-items: center;
}
.bottom__title {
  font-family: "Roboto", sans-serif;
  color: #3f3f3f;
  font-size: 18px;
  // margin-bottom: 30px;
  margin-bottom: 14px;
  padding-bottom: 8px;
  width: fit-content;
}
.weather__info {
  display: flex;
  margin-left: -3.5vw;
  // flex-direction: column;
}
// .column:first-of-type .bottom__title {
//   border-bottom: 2px solid #3f3f3f;
//   margin-bottom: 20px;
// }
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
    // margin-bottom: 4vh;
    // padding-bottom: 16px;
    // border-bottom: 2px solid #3f3f3f;
  }
  .weather__info {
    margin-left: -12px;
  }
  .bottom__title {
    margin-bottom: 8px;
  }
}
@media only screen 
and (min-device-width : 414px) 
and (max-device-width : 736px) { 
  .top__header {
    height: 23vh;
  }
}
</style>
