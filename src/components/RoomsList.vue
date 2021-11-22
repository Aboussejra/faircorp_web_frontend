<template>
  <div class="rooms-list pt-3">
    <rooms-list-item v-for="room in rooms" :room="room" :key="room.id">
    </rooms-list-item>
  </div>
</template>


<script>
import axios from "axios";
import { API_HOST } from "../config";
import roomsListItem from "./RoomsListItem";

export default {
  components: {
    roomsListItem,
  },
  name: "roomsList",
  data: function () {
    return {
      // rooms initialised as an empty array, until data is retrieved from the API
      rooms: [],
    };
  },
  created: async function () {
    let response = await axios.get(`${API_HOST}/api/rooms`);
    let rooms = response.data;
    this.rooms = rooms;
  },
  methods: {
    updateroom(newroom) {
      // Find rooms and replace it with the new info after potential update from the user
      let index = this.rooms.findIndex((room) => room.id === newroom.id);
      this.rooms.splice(index, 1, newroom);
    },
  },
};
</script>
