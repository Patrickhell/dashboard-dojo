<template>
  <LineChartGenerator
    v-if="loaded"
    :data="chartData"
    :options="chartOptions"
    :chart-id="chartId"
    :dataset-id-key="datasetIdKey"
    :plugins="plugins"
    :css-classes="cssClasses"
    :styles="styles"
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
    datasetIdKey: {
      type: String,
      default: "label",
    },
    width: {
      type: Number,
      default: 600,
    },
    height: {
      type: Number,
      default: 150,
    },
    cssClasses: {
      default: "",
      type: String,
    },
    styles: {
      type: Object,
      default: () => {},
    },
    plugins: {
      type: Array,
      default: () => [],
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
            backgroundColor: "#e0ebed",
            borderColor: "#9ebfc5",
            pointBackgroundColor: "#9ebfc5",
            data: [],
          },
        ],
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
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
