<template>
  <LineChartGenerator
    v-if="loaded"
    :data="chartData"
    :options="chartOptions"
    :chart-id="chartId"
    :width="width"
    :height="height"
  />
</template>
<script>
import axios from "axios";
import { Line as LineChartGenerator } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  CategoryScale,
  PointElement,
} from "chart.js";
ChartJS.register(
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  CategoryScale,
  PointElement
);
const getUrl = "https://api.jsonbin.io/v3/b/6528a5f012a5d376598b094c"; // request URL
const token = "$2a$10$pSgYR7heD8q/g4lbvy7QR.2QAlkkn19qEFW2z7MwRaFvKbgG2bWSu"; // access token
var axiosHeaders = {
  headers: { "X-MASTER-KEY": token },
};
export default {
  name: "LineChart",
  components: { LineChartGenerator },
  props: {
    chartId: {
      type: String,
      default: "line-chart",
    },
    width: {
      type: Number,
      default: 600,
    },
    height: {
      type: Number,
      default: 150,
    },
  },
  data() {
    return {
      loaded: false,
      chartData: {
        labels: [],
        datasets: [
          {
            label: "Montly",
            borderColor: "#9ebfc5",
            pointBackgroundColor: "#9ebfc5",
            data: [],
            backgroundColor: ["#e0ebed"],
          },
        ],
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
        layout: {
          padding: {
            left: 40,
            right: 40,
          },
        },
        plugins: {
          title: {
            display: true,
            text: "Monthly Connections",
          },
        },
      },
    };
  },
  async mounted() {
    axios
      .get(getUrl, axiosHeaders)
      .then((response) => {
        console.log(response.data.record.MonthlyConnections);
        const results = response.data.record.MonthlyConnections;
        results.forEach((item) => {
          this.chartData.labels.push(item.month);
          this.chartData.datasets[0].data.push(item.connections);
          this.loaded = true;
        });
        console.log(this.chartData.labels);
        console.log(this.chartData.datasets[0].data);
      })
      .catch(function (error) {
        console.log(error);
      });
  },
};
</script>
