<template>
  <div>
    <div class="navbar d-flex justify-content-between">
      <ul>
        <li>
          <i class="fa-solid fa-bars margin-right"></i>
        </li>
      </ul>
      <ul class="d-flex margin">
        <li>
          <i class="fa-regular fa-envelope margin-right"></i>
        </li>
        <li>
          <img class="margin-right" src="../assets/avatar.png" alt="avatar" />
        </li>
        <li class="fw-semibold">Mario rossi</li>
        <li>
          <i class="fa-solid fa-angle-down"></i>
        </li>
      </ul>
    </div>
    <div class="chartLine-content">
      <LineChartGenerator />
    </div>
    <div class="barLine-content">
      <BarChart />
    </div>
  </div>
</template>
<script>
import LineChartGenerator from "@/components/Line.vue";
import BarChart from "@/components/Bar.vue";
export default {
  name: "MainSide",
  components: { LineChartGenerator, BarChart },
  props: {
    nav: String,
  },
};
</script>
<style scoped lang="scss">
ul {
  list-style: none;
}
img {
  width: 30px;
  height: 30px;
  border-radius: 50%;
}
.margin {
  padding-right: 1.8rem;
}
.margin-right {
  margin-right: 0.8rem;
}
.navbar {
  background-color: #ededed;
  height: 50px;
}
</style>
