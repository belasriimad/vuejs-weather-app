<template>
  <div class="container">
    <Search @search-result="getWeather" />
    <CurrentWeather :weather="state.weather" />
    <ComingDays :data="state.data" />
  </div>
</template>

<script>
import Search from "./Search.vue";
import CurrentWeather from "./CurrentWeather.vue";
import ComingDays from "./ComingDays.vue";
import { reactive } from "vue";

export default {
  name: "Home",
  components: { Search, CurrentWeather, ComingDays },
  setup() {
    const state = reactive({
      weather: null,
      data: null,
      key: "1d5cfbb4b1ba74f6287033207b5f59d7",
    });

    async function getWeather(city) {
      const proxy = "https://cors-anywhere.herokuapp.com/";
      const apiURL = `https://api.darksky.net/forecast/${state.key}/${city.latlng.lat},${city.latlng.lng}?lang=fr&units=ca`;
      const data = await fetch(proxy + apiURL);
      const resData = await data.json();
      const weatherData = {
        time: resData.currently.time,
        summary: resData.currently.summary,
        icon: `${resData.currently.icon}.png`,
        temperature: `${Math.round(resData.currently.temperature)}˚C`,
        humidity: resData.currently.humidity,
      };
      state.weather = weatherData;
      state.data = resData.daily.data;
    }

    return {
      getWeather,
      state,
    };
  },
};
</script>

<style>
body {
  background: #ccc;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}
</style>
