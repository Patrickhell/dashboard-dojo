<template>
  <div>
    <button @click="fillData()" class="play-button">
      <i class="fa-solid fa-play"></i>
    </button>
    <div class="chart-content" id="myChart">
      <SolarLineChart
        :data="chartData"
        :options="chartOptions"
        :chart-id="chartId"
        :width="width"
        :height="height"
      />
    </div>
  </div>
</template>
<script>
import { Line as SolarLineChart } from "vue-chartjs";
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
export default {
  name: "LineChart",
  components: { SolarLineChart },
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
      default: 300,
    },
  },
  data() {
    return {
      //impostiamo chartData su null e nel metodo created() aggiungiamo fillData()
      //in questo modo, ogni volta che vienne creata l'istanza del componente
      //la funzione fillData viene creata nell'oggetto methods
      chartData: null,
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
            text: "Solar Power",
          },
        },
      },
    };
  },
  created() {
    this.fillData();
  },
  methods: {
    //inizializziamo un metodo che ci permette di configurare il nostro grafico
    fillData() {
      (this.chartData = {
        //generariamo una array da 1 a 23 ettichette
        labels: Array.from({ length: 23 }, (_, i) => i + 1),
        datasets: [
          {
            label: "Daily",
            borderColor: "#9ebfc5",
            pointBackgroundColor: "#9ebfc5",
            //generiamo un array di numeri casuali (asse Y) compresi da 0 a 100
            // grazie al metodo getRandomInt()
            data: [0].concat(
              Array.from({ length: 23 }, () => this.getRandomIntWithVariation())
            ),
            backgroundColor: ["#e0ebed"],
          },
        ],
      }),
        this.chartOptions;
    },
    //generiamo un numero casuale con una variazione random compresa tra 0 e 5
    getRandomIntWithVariation() {
      // generiamo un Numero casuale tra 0 e 100
      const baseValue = Math.floor(Math.random() * 101);
      //Calcoliamo il 5% della cifra generata casualmente
      const variationPercent = (baseValue * 5) / 100;
      //Generiamo un valore casuale tra -1 e 1 (per la variazione negativa o positiva)
      const randomSign = Math.random() < 0.5 ? -1 : 1;
      //Calcoliamo la variazione effettiva
      const variation = variationPercent * randomSign;
      //Aggiungiamo la variazione al valore base
      const finalValue = baseValue + variation;
      //verifichiamo che il risultato sia compreso tra 0 e 100
      return Math.min(100, Math.max(0, finalValue));
    },
  },
};
</script>
<style lang="scss" scoped>
.play-button {
  margin-bottom: 4rem;
}
</style>
