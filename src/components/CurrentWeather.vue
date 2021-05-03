<template>
  <div className="weather border-bottom" v-if="weather">
    <div className="weather-header">
      <img
        :src="state.iconLink + weather.icon"
        alt="icon"
        width="80"
        height="80"
        className="img-fluid"
      />
      <h3 className="temperature font-weight-bold">
        {{ weather.temperature }}
      </h3>
    </div>
    <h3 className="temperature my-2 font-weight-bold">
      {{ state.currentDate }}
    </h3>
    <h5 className="font-weight-bold">{{ weather.summary }}</h5>
  </div>
</template>

<script>
import { reactive } from "vue";
import moment from "moment";
import "moment/locale/fr";

export default {
  props: {
    weather: Object,
  },
  setup() {
    const state = reactive({
      iconLink: "https://darksky.net/images/weather-icons/",
      currentDate: moment().calendar(),
    });

    return {
      state,
    };
  },
};
</script>

<style scoped>
.weather {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
}
.weather-header {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  width: 100%;
}
</style>
