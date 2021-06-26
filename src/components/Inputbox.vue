<template>
  <div>
    <input type="text" v-model="ipaddr" />
    <p @click="changeIP">></p>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      ipaddr: "8.8.8.8",
    };
  },
  methods: {
    getIP: function () {
      fetch(
        `https://geo.ipify.org/api/v1?apiKey=at_IzJTorIbvzjfGBVdYiUPHx1LrPPsa&ipAddress=${this.ipaddr}`
      )
        .then((response) => response.json())
        .then((data) => {
          let details = {
            ip: data.ip,
            location: `${data.location.city}, ${data.location.region}`,
            timezone: `UTC${data.location.timezone}`,
            isp: data.isp,
            lat: parseInt(data.location.lat),
            lng: parseInt(data.location.lng),
          };
          //console.table(details);
          this.$emit("show-ip-details", details);
        });
    },
    changeIP: function () {
      this.getIP();
    },
  },
};
</script>

<style scoped>
div {
  background: none;
  position: relative;
  height: 100%;
}

input {
  padding: 5px 20px;
  border-radius: 10px;
  height: 100%;
}

p {
  position: absolute;
  background-color: black;
  color: white;
  border-radius: 0px 10px 10px 0px;
  right: 0;
  width: 2rem;
  text-align: center;
  font-size: bold;
  padding: 15px;
  height: 100%;
  vertical-align: middle;
}
</style>
