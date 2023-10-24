<template>
  <div>
    <DoughnutGenerator
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
import { Doughnut as DoughnutGenerator } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  ArcElement,
  CategoryScale,
} from "chart.js";
ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale);
const getUrl = "https://api.jsonbin.io/v3/b/6536775a12a5d376598f6d50"; // request URL
const token = "$2a$10$pSgYR7heD8q/g4lbvy7QR.2QAlkkn19qEFW2z7MwRaFvKbgG2bWSu"; // access token
var axiosHeaders = {
  headers: { "X-MASTER-KEY": token },
};
export default {
  name: "DoughnutChart1",
  components: {
    DoughnutGenerator,
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
          title: {
            display: true,
            text: "Operating System",
          },
        },
      },
    };
  },
  async mounted() {
    axios
      .get(getUrl, axiosHeaders)
      .then((response) => {
        console.log(response.data.record);
        const results = response.data.record;
        // Creare un oggetto per tenere traccia del conteggio per ciascun sistema operativo
        const deviceObject = {};
        // Itera attraverso i dati e aggiorna il conteggio per ciascun sistema operativo
        results.forEach((item) => {
          const operativeSystemName = item.device;
          // Verifica se l'intervallo di età è già nell'oggetto conteggioPerEta
          if (deviceObject[operativeSystemName]) {
            deviceObject[operativeSystemName] += 1;
          } else {
            deviceObject[operativeSystemName] = 1;
          }
        });
        //Converti l'oggetto conteggioPerEta in un array di oggetti
        const data = Object.keys(deviceObject).map((operativeSystemName) => ({
          device: operativeSystemName,
          numberOfoperativeSystem: deviceObject[operativeSystemName],
        }));
        console.log(data);
        data.forEach((element) => {
          this.chartData.labels.push(element.device);
          this.chartData.datasets[0].data.push(element.numberOfoperativeSystem);
          this.loaded = true;
        });
      })
      .catch(function (error) {
        console.log(error);
      });
  },
};
</script>
