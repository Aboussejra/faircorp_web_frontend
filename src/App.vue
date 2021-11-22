<template>
  <div id="app">
    <header>
      <h1>Boussejra Amir Faircorp Web App</h1>
      <p class="lead">
        Web App to view and manage Windows, Rooms and Heaters from Faircorp
        Spring Backend
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
  color: #7c795d;
  font-family: "Trocchi", serif;
  font-size: 45px;
  font-weight: normal;
  line-height: 48px;
  margin: 0;
}
p {
  color: #525252;
  font-family: "Source Sans Pro", sans-serif;
  font-size: 16px;
  line-height: 32px;
  margin: 0 0 24px;
}
</style>
