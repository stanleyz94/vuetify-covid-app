<template>
  <v-card class="a elevation-0 rounded-lg pa-5" max-width="870">
    <horizontal-bar :chart-data="chartdata" :options="options"></horizontal-bar>
  </v-card>
</template>

<script>
import HorizontalBar from './HorizontalBar.js';
export default {
  components: {
    HorizontalBar,
  },

  data() {
    return {
      loaded: false,
      chartdata: null,
      gradient: null,
      regions: [],
      infected: [],
      options: {
        scales: {
          yAxes: [
            {
              ticks: {
                beginAtZero: true,
              },
              gridLines: {
                display: false,
              },
            },
          ],
          xAxes: [
            {
              gridLines: {
                display: true,
              },
            },
          ],
        },
        legend: {
          display: true,
        },
        responsive: true,
        maintainAspectRatio: false,
      },
    };
  },
  methods: {
    fillChartWithData() {
      this.chartdata = {
        labels: this.regions,
        datasets: [
          {
            label: 'Łączna liczba zakażen',
            borderColor: '#FC2525',
            pointBackgroundColor: 'white',
            borderWidth: 1,
            pointBorderColor: 'white',
            backgroundColor: this.gradient,
            data: this.infected,
          },
        ],
      };
    },

    async fillDataAPI() {
      try {
        const response = await fetch(
          'https://api.apify.com/v2/key-value-stores/3Po6TV7wTht4vIEid/records/LATEST?disableRedirect=true'
        );
        const responseData = await response.json();
        const emptyArray = [];
        responseData.infectedByRegion.forEach((region) => {
          emptyArray.push({
            region: region.region,
            infectedCount: region.infectedCount,
          });
        });

        emptyArray
          .sort((a, b) => b.infectedCount - a.infectedCount)
          .map((region) => {
            this.regions.push(region.region);
            this.infected.push(region.infectedCount);
          });

        this.fillChartWithData();
      } catch (e) {
        console.error(e);
      }
    },
    addGradient() {
      this.gradient = document
        .getElementById('horizontalbar-chart')
        .getContext('2d')
        .createLinearGradient(0, 0, 0, 450);

      this.gradient.addColorStop(0, 'rgba(255, 61, 61, 1)');
      this.gradient.addColorStop(0.5, 'rgba(255, 0, 0, 0.25)');
      this.gradient.addColorStop(1, 'rgba(255, 0, 0, 0)');
    },
  },
  mounted() {
    this.fillDataAPI();
    this.addGradient();
    this.fillChartWithData();
  },
};
</script>
