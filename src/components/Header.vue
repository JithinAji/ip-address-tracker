<template>
  <div>
    <h1>{{ title }}</h1>
    <Inputbox @show-ip-details="changeIp" class="inputbox" />
    <Card class="card" v-model:data.sync="data" />
  </div>
</template>

<script>
import Inputbox from "./Inputbox.vue";
import Card from "./Card.vue";

export default {
  data: function () {
    return {
      title: "IP Address Tracker",
      data: {
        ip: "",
        location: "",
        timezone: "",
        isp: "",
      },
    };
  },
  components: {
    Inputbox,
    Card,
  },
  methods: {
    changeIp: function (details) {
      this.data = details;
      this.$emit("locate-map", { lat: details.lat, lng: details.lng });
    },
  },
};
</script>


<style scoped>
div {
  height: 30vh;
  display: flex;
  flex-direction: column;
  width: 100%;
  background-image: url("../assets/pattern-bg.png");
  background-repeat: no-repeat;
  background-size: cover;
}

h1 {
  color: white;
  font-size: 1.5rem;
  width: 100%;
  text-align: center;
  margin-top: 5%;
}

.inputbox {
  width: 40%;
  min-width: 250px;
  margin: 15px auto;
  min-height: 50px;
  border-radius: 10px;
}

.card {
  margin: 20px auto;
  width: 90%;
  z-index: 1000;
}

@media (min-width: 801px) {
  .card {
    width: 60%;
  }
}
</style>