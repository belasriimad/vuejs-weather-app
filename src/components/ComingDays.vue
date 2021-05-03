<template>
  <div className="row mt-3 mx-auto" v-if="data">
    <div className="col-md-2 mb-1" v-for="day in data" :key="day.time">
      <div className="day shadow rounded">
        <span className="text-dark">
          {{ convertTimestamp(day.time) }}
        </span>
        <img
          :src="state.iconLink + day.icon + '.png'"
          alt="icon"
          width="50"
          height="50"
          className="img-fluid"
        />
        <span className="text-dark">
          Max: {{ Math.round(day.temperatureHigh) + "˚C" }}
        </span>
        <span className="text-dark">
          Min: {{ Math.round(day.temperatureLow) + "˚C" }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from "vue";
import moment from "moment";
import "moment/locale/fr";

export default {
  props: {
    data: Object,
  },
  setup() {
    const state = reactive({
      iconLink: "https://darksky.net/images/weather-icons/",
    });

    function convertTimestamp(time) {
      let day = moment
        .unix(time)
        .locale("fr")
        .utc();
      return day.format("dddd MMM Do");
    }

    return {
      state,
      convertTimestamp,
    };
  },
};
</script>

<style scoped>
.day {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 10px;
  background-color: beige;
  height: 150px;
  width: 150px;
}
</style>
