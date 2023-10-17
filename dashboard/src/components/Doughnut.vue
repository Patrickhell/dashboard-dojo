<template>
  <div>
    <Doughnut
      v-if="loaded"
      :data="chartData"
      :options="chartOptions"
      :chart-id="chartId"
      :plugins="plugins"
      :css-classes="cssClasses"
      :styles="styles"
      :width="width"
      :height="height"
      label="Operating System"
    />
  </div>
</template>
<script>
import axios from "axios";
import { Doughnut } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  ArcElement,
  CategoryScale,
} from "chart.js";
ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale);
const getUrl = "https://api.jsonbin.io/v3/b/6528a5f012a5d376598b094c"; // request URL
const token = "$2a$10$pSgYR7heD8q/g4lbvy7QR.2QAlkkn19qEFW2z7MwRaFvKbgG2bWSu"; // access token
var axiosHeaders = {
  headers: { "X-MASTER-KEY": token },
};
export default {
  name: "DoughnutChart",
  components: {
    Doughnut,
  },
  props: {
    chartId: {
      type: String,
      default: "bar-chart",
    },
    width: {
      type: Number,
      default: 500,
    },
    height: {
      type: Number,
      default: 200,
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
    label: {
      type: String,
      default: "User Age Range",
    },
  },
  data() {
    return {
      loaded: false,
      chartData: {
        labels: [],
        datasets: [
          {
            label: this.label,
            data: [],
            backgroundColor: [
              "#3e95cd",
              "#8e5ea3",
              "#5abb9f",
              "#e8c3b9",
              "#c45850",
            ],
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
          autoPadding: true,
        },
        plugins: {
          legend: {
            display: true,
            align: "center",
            position: "right",
          },
        },
      },
    };
  },
  async mounted() {
    axios
      .get(getUrl, axiosHeaders)
      .then((response) => {
        console.log(response.data.record.Devices);
        const results = response.data.record.Devices;
        results.forEach((item) => {
          this.chartData.labels.push(item.os);
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
