<template>
  <div class="container-fluid">
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
    <div class="barLine_doughnut-content d-flex">
      <div>
        <BarChart />
      </div>
      <div>
        <DoughnutChart />
      </div>
    </div>
    <div>
      <div class="SolarChart-content">
        <SolarLineChart />
      </div>
    </div>
    <div class="d-flex">
      <div>
        <BarChartGenerator />
      </div>
      <div>
        <DoughnutGenerator />
      </div>
    </div>
  </div>
</template>
<script>
import LineChartGenerator from "@/components/Line.vue";
import BarChart from "@/components/Bar.vue";
import DoughnutChart from "@/components/Doughnut.vue";
import SolarLineChart from "@/components/LineChart.vue";
import BarChartGenerator from "@/components/BarChart.vue";
import DoughnutGenerator from "@/components/DoughnutChart.vue";
export default {
  name: "MainSide",
  components: {
    LineChartGenerator,
    BarChart,
    DoughnutChart,
    SolarLineChart,
    BarChartGenerator,
    DoughnutGenerator,
  },
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
  width: calc(100vw - 200px);
}
.chartLine-content {
  margin-top: 4rem;
  margin-bottom: 6rem;
}
.barLine_doughnut-content {
  margin-bottom: 10rem;
}
.SolarChart-content {
  margin-bottom: 5rem;
}
</style>
