<template>
  <div id="app">
    <header>
      <h1>Boussejra Amir Faircorp Web App</h1>
      <p class="lead">
        This app is dedicated to viewing the Windows, Rooms and Heaters from the
        App we built in the previous courses
      </p>
    </header>

    <section class="w-50 mx-auto">
      <button
        v-for="option in options"
        :key="option"
        @click="base_selected = option"
        class="btn btn-dark ms-2"
      >
        {{ option }}
      </button>
      <component :is="base_selected"></component>
    </section>
  </div>
</template>


<script>
import WindowsList from "./components/WindowsList.vue";
import RoomsList from "./components/RoomsList.vue";
import HeatersList from "./components/HeatersList.vue";

export default {
  name: "App",
  components: {
    WindowsList,
    RoomsList,
    HeatersList,
  },
  data: function () {
    return {
      options: ["WindowsList", "RoomsList", "HeatersList"],
      base_selected: "WindowsList",
    };
  },
};
</script>

<style lang="scss" scoped>
#app {
  font-family: Helvetica;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 50px;
}

h1 {
  text-align: center;
  font-family: Helvetica;
  font-size: 60px;
  letter-spacing: 4px;
  word-spacing: -7px;
  color: black;
}
</style>
