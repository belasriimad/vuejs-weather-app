<template>
  <div className="row mt-4">
    <div className="col-md-6 mx-auto">
      <div className="form-group">
        <input
          type="search"
          name="city"
          id="address-input"
          autoComplete="off"
          className="form-control"
          placeholder="Entrer une ville"
          aria-describedby="helpId"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, reactive } from "vue";
import places from "places.js";

export default {
  emits: ["search-result"],
  setup(props, { emit }) {
    const state = reactive({
      appId: "pl84BDTK7HU7",
      apiKey: "671cd803cf905b98ff3217c773e5207a",
    });

    function getPlaces() {
      let placesAutocomplete = places({
        appId: state.appId,
        apiKey: state.apiKey,
        container: document.querySelector("#address-input"),
      });
      placesAutocomplete.on("change", function($event) {
        emit("search-result", $event.suggestion);
      });
    }

    onMounted(() => {
      getPlaces();
    });

    return {};
  },
};
</script>

<style scoped></style>
