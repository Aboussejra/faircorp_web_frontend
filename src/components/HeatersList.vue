<template>
  <div class="heaters-list pt-4">
    <heaters-list-item
      v-for="heater in heaters"
      :heater="heater"
      :key="heater.id"
      @heater-updated="updateHeater"
    >
    </heaters-list-item>
  </div>
</template>


<script>
import axios from "axios";
import { API_HOST } from "../config";
import HeatersListItem from "./HeatersListItem";

export default {
  components: {
    HeatersListItem,
  },
  name: "HeatersList",
  data: function () {
    return {
      // heaters initialised as an empty array, until data is retrieved from the API
      heaters: [],
    };
  },
  created: async function () {
    let response = await axios.get(`${API_HOST}/api/heaters`);
    let heaters = response.data;
    this.heaters = heaters;
    console.log(heaters);
  },
  methods: {
    updateHeater(newHeater) {
      // Find heater in the array, and replace it with the new info after potential update from the user
      let index = this.heaters.findIndex(
        (heater) => heater.id === newHeater.id
      );
      this.heaters.splice(index, 1, newHeater);
    },
  },
};
</script>
