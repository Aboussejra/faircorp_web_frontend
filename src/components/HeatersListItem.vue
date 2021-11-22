<template>
  <div
    class="border border-info rounded p-2 mb-2"
    :class="{ expanded: isExpanded }"
  >
    <div class="top-row d-flex" @click="toggleExpand">
      <div class="fw-bold pe-3">{{ heater.name }}</div>
      <div class="text-muted">{{ heater.roomName }}</div>
      <div class="ms-3">Power : {{ heater.power }}</div>
      <div
        class="status ms-4"
        :class="{ open: isHeaterOn, closed: !isHeaterOn }"
      >
        <template v-if="isHeaterOn">
          <span class="icon">&#x2B24;</span> On
        </template>
        <template v-else> <span class="icon">&#x2716;</span> Off </template>
      </div>

      <div class="ms-auto">
        {{ isExpanded ? "&#128315;" : "&#9658;" }}
      </div>
    </div>
    <template v-if="isExpanded">
      <hr />
      <div class="details d-flex">
        <button
          type="button"
          class="btn btn-secondary me-2"
          @click="switchHeater"
        >
          Turn {{ isHeaterOn ? "Off" : "On" }} heater
        </button>
      </div>
    </template>
  </div>
</template>
 
<script>
import axios from "axios";
import { API_HOST } from "../config";

export default {
  name: "HeatersListItem",
  props: ["heater"],
  data: function () {
    return {
      isExpanded: false,
    };
  },
  computed: {
    isHeaterOn: function () {
      return this.heater.heaterStatus === "ON";
    },
  },
  methods: {
    toggleExpand() {
      this.isExpanded = !this.isExpanded;
    },
    async switchHeater() {
      let response = await axios.put(
        `${API_HOST}/api/heaters/${this.heater.id}/switch`
      );
      let updatedHeater = response.data;
      this.$emit("heater-updated", updatedHeater);
    },
  },
};
</script>

<style lang="scss" scoped>
.status {
  .icon {
    position: relative;
  }

  &.open {
    color: #128b53;
    .icon {
      font-size: 12px;
      top: -3px;
    }
  }

  &.closed {
    color: #df2134;
  }
}

.heater {
  .top-row {
    cursor: pointer;
  }
}
</style>
