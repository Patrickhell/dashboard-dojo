<template>
  <div>
    <Bar
      v-if="loaded"
      :data="chartData"
      :options="chartOptions"
      :chart-id="chartId"
      :width="width"
      :height="height"
    />
  </div>
</template>
<script>
import axios from "axios";
import { Bar } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  LinearScale,
  CategoryScale,
} from "chart.js";
ChartJS.register(
  Title,
  Tooltip,
  Legend,
  BarElement,
  LinearScale,
  CategoryScale
);
const getUrl = "https://api.jsonbin.io/v3/b/6528a5f012a5d376598b094c"; // request URL
const token = "$2a$10$pSgYR7heD8q/g4lbvy7QR.2QAlkkn19qEFW2z7MwRaFvKbgG2bWSu"; // access token
var axiosHeaders = {
  headers: { "X-MASTER-KEY": token },
};
export default {
  name: "BarChart",
  components: {
    Bar,
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
      default: 250,
    },
  },
  data() {
    return {
      loaded: false,
      chartData: {
        labels: [],
        datasets: [
          {
            label: "",
            data: [],
            backgroundColor: [
              "#3e95cd",
              "#8e5ea3",
              "#5abb9f",
              "#E8c3b9",
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
        },
        plugins: {
          title: {
            display: true,
            text: "User Age Range",
          },
          legend: {
            display: false,
          },
        },
      },
    };
  },
  async mounted() {
    axios
      .get(getUrl, axiosHeaders)
      .then((response) => {
        console.log(response.data.record.UsersAgeRange);
        const results = response.data.record.UsersAgeRange;
        results.forEach((item) => {
          this.chartData.labels.push(item.range);
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
