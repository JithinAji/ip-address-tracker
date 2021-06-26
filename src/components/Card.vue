<template>
  <div class="card">
    <div>
      <p class="title">IP Adress</p>
      <p class="desc">{{ data.ip }}</p>
    </div>
    <div class="markright">
      <p class="title">LOCATION</p>
      <p class="desc">{{ data.location }}</p>
    </div>
    <div class="markright">
      <p class="title">TIMEZONE</p>
      <p class="desc">{{ data.timezone }}</p>
    </div>
    <div class="markright">
      <p class="title">ISP</p>
      <p class="desc">{{ data.isp }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  data: function () {
    return {};
  },
  props: {
    data: {
      type: Object,
      default: () => ({}),
    },
  },
};
</script>

<style scoped>
.card {
  background: white !important;
  width: 100%;
  min-height: 130px;
  text-align: center;
  border-radius: 10px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-items: center;
  flex-direction: row;
}

.markright {
  border-left: 1px solid var(--darkgray);
  padding-left: 1.5rem;
}

.title {
  color: var(--darkgray);
  text-align: left;
  width: 100%;
  font-weight: 700;
  font-size: 0.8rem;
  margin-bottom: 5px;
}

.desc {
  font-weight: 700;
}

@media (max-width: 801px) {
  .card {
    flex-direction: column;
    height: 400px;
    min-height: 250px;
  }
  .card div {
    width: 100%;
    margin-bottom: 0.5rem;
  }
  .markright {
    border-left: none;
    padding-left: none;
  }
  .title {
    text-align: center;
  }
}
</style>