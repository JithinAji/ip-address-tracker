<!-- 
Main app.js componet
child components - Header, Maps
-->

<template>
  <Header @locate-map="locateMap"></Header>
  <Maps v-model:lat.sync="lat" v-model:lng.sync="lng"></Maps>
</template>

<script>
import Header from "./components/Header.vue";
import Maps from "./components/Maps.vue";

export default {
  name: "App",
  data: function () {
    return {
      lat: null,
      lng: null,
    };
  },
  components: {
    Header,
    Maps,
  },
  methods: {
    locateMap: function (locate) {
      this.lat = locate.lat;
      this.lng = locate.lng;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Rubik:wght@400;500;700&display=swap");

:root {
  --verydarkgray: hsl(0, 0%, 17%);
  --darkgray: hsl(0, 0%, 59%);
}

* {
  margin: 0;
  padding: 0;
  font-family: "Rubik", sans-serif;
  font-size: 18px;
  outline: none;
  box-sizing: border-box;
}
</style>
