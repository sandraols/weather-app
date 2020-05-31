<template>
  <div>
    <FirstPage v-if="!gotWeather" :city="city" @input="city = $event" @getWeather="getWeather()"></FirstPage>
    <SecondPage v-else :weather="weather" :city="city" @input="city = $event" @getWeather="getWeather()"></SecondPage>
  </div>
</template>

<script>
import axios from 'axios';
import FirstPage from "./components/FirstPage.vue";
import SecondPage from "./components/SecondPage.vue";

export default {
  name: "App",
  data: function() {
    return {
      weather: null,
      gotWeather: false,
      city: "",
    };
  },
  methods: {
    getWeather() {
      console.log('getWeather')
      axios
      .get(`https://api.openweathermap.org/data/2.5/forecast?q=${this.city}&units=metric&appid=75d52df782aadd749ed253cf966cb823`)
      .then(response => {
        this.weather = response.data;
        this.gotWeather = true;
        console.log(this.weather)
      })
    }
  },
  components: {
    FirstPage,
    SecondPage,
  }
};
</script>

<style lang="scss">
$header-font: "Rubik", sans-serif;
$paragraph-font: "Roboto", sans-serif;

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>

