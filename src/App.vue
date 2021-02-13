<template>
  <div>
    <EquityDetails v-bind:equity-details="this.equityDetails" />
  </div>
</template>
<script>
import EquityDetails from "./components/EquityDetails";
import axios from "axios";

export default {
  name: "App",
  components: {
    EquityDetails,
  },
  data: function () {
    return {
      equityDetails: [],
      errors: [],
    };
  },
  created() {
    axios
      .get("http://localhost:8000/info")
      .then((response) => {
        this.equityDetails = response.data;
      })
      .catch((e) => this.errors.push(e));
  },
};
</script>

<style>
.app {
  font-family: Arial, Helvetica, sans-serif;
}
</style>
