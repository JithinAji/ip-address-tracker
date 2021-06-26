<!--
Map component
gets latitude and longitude from app.vue
-->

<template>
  <div id="mapContainer"></div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";

export default {
  name: "LeafletMap",
  props: {
    lat: null,
    lng: null,
  },
  data() {
    return {
      map: null,
      marker: null,
    };
  },

  watch: {
    lat: function (newVal) {
      this.setMap(newVal, this.lng);
    },
    lng: function (newVal) {
      this.setMap(this.lat, newVal);
    },
  },
  methods: {
    setMap: function (lat, lng) {
      this.map.setView([lat, lng]);
      this.marker.setOpacity(1);
      this.marker.setLatLng([lat, lng], { opacity: 1 });
    },
  },

  mounted() {
    //here's the SVG for the marker
    var icon = `<svg xmlns="http://www.w3.org/2000/svg" width="46" height="56"><path fill-rule="evenodd" d="M39.263 7.673c8.897 8.812 8.966 23.168.153 32.065l-.153.153L23 56 6.737 39.89C-2.16 31.079-2.23 16.723 6.584 7.826l.153-.152c9.007-8.922 23.52-8.922 32.526 0zM23 14.435c-5.211 0-9.436 4.185-9.436 9.347S17.79 33.128 23 33.128s9.436-4.184 9.436-9.346S28.21 14.435 23 14.435z"/></svg>`;

    // here's the trick, base64 encode the URL
    var svgURL = "data:image/svg+xml;base64," + btoa(icon);

    // create icon
    var mySVGIcon = L.icon({
      iconUrl: svgURL,
      iconSize: [30, 40],
      shadowSize: [12, 10],
      iconAnchor: [5, 5],
      popupAnchor: [5, -5],
    });

    this.map = L.map("mapContainer").setView([51.4934, 0.0098], 12);
    L.tileLayer("http://{s}.tile.osm.org/{z}/{x}/{y}.png", {
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
    }).addTo(this.map);

    this.marker = L.marker([51.4934, 0.0098], {
      icon: mySVGIcon,
      opacity: 0,
    }).addTo(this.map);
    this.marker.setOpacity(0);
  },
  beforeUnmount() {
    if (this.map) {
      this.map.remove();
    }
  },
};
</script>

<style scoped>
#mapContainer {
  width: 100vw;
  height: 70vh;
}
</style>
