<template>
  <div class="windows-list pt-4">
    <windows-list-item
      v-for="window in windows"
      :window="window"
      :key="window.id"
      @window-updated="updateWindow"
    >
    </windows-list-item>
  </div>
</template>


<script>
import axios from "axios";
import { API_HOST } from "../config";
import WindowsListItem from "./WindowsListItem";

export default {
  components: {
    WindowsListItem,
  },
  name: "WindowsList",
  data: function () {
    return {
      // windows initialised as an empty array, until data is retrieved from the API
      windows: [],
    };
  },
  created: async function () {
    let response = await axios.get(`${API_HOST}/api/windows`);
    let windows = response.data;
    this.windows = windows;
  },
  methods: {
    updateWindow(newWindow) {
      // Find window, and replace it with the new info after potential update from the user
      let index = this.windows.findIndex(
        (window) => window.id === newWindow.id
      );
      this.windows.splice(index, 1, newWindow);
    },
  },
};
</script>
