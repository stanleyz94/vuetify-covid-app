<template>
  <v-card flat height="100%" class="pa-5 white rounded-lg">
    <div class="d-flex align-center">
      <h3 class=" mb-0 font-weight-bold text-center">
        Mapa zakażeń COVID-19
      </h3>
      <v-badge left class="ml-auto caption" color="red my-2" inline tile>
        Najbardziej dotknięte
      </v-badge>
      <v-badge class="caption" left color="red lighten-4 my-2" inline tile>
        Najmniej dotknięte
      </v-badge>
    </div>

    <div v-show="!loadingMap">
      <GChart
        type="GeoChart"
        :data="chartData"
        :options="chartOptions"
        :settings="{ packages: ['geochart'], mapsApiKey: 'EMPTY' }"
      />
      <v-progress-circular
        v-show="loadingMap"
        :style="{ top: '45%', left: '45%', position: 'absolute' }"
        indeterminate
        :size="70"
        :width="7"
        color="red lighten-1"
      ></v-progress-circular>
      <div v-show="$vuetify.breakpoint.smAndUp">
        <v-card
          :style="{
            top: '23%',
            left: '8%',
            position: 'absolute',
          }"
          elevation="0"
          class="rounded-lg"
        >
          <v-btn width="45" height="45" color="red" icon>
            <v-icon rigth>mdi-magnify</v-icon>
          </v-btn>
        </v-card>

        <v-card
          :style="{
            top: '23%',
            left: '80%',
            position: 'absolute',
          }"
          class="rounded-lg d-flex flex-column"
          elevation="0"
        >
          <v-btn width="45" height="45" color="red" icon>
            <v-icon rigth>mdi-plus</v-icon>
          </v-btn>
          <v-divider></v-divider>
          <v-btn width="45" height="45" color="red" icon>
            <v-icon rigth>mdi-minus</v-icon>
          </v-btn>
        </v-card>
      </div>
    </div>
  </v-card>
</template>

<script>
import { GChart } from 'vue-google-charts';
export default {
  components: {
    GChart,
  },
  data() {
    return {
      secondUrl:
        'https://api.apify.com/v2/key-value-stores/3Po6TV7wTht4vIEid/records/LATEST?disableRedirect=true',

      loading: false,
      loadingMap: false,
      chartData: [
        [
          'Wojewodztwa',
          'Łączna liczba zakażeń',
          'Łączna liczba przypadków śmiertelnych',
        ],
        // ['Pomorskie', 200, 2],
        // ['Kujawsko-Pomorskie', 300, 3],
        // ['Dolnoslaskie', 400, 5],
        // ['Lubelskie', 500, 7],
        // ['Lodzkie', 600, 9],
        // ['Malopolskie', 300, 2],
        // ['Mazowieckie', 400, 5],
        // ['Opolskie', 700, 3],
        // ['Podkarpackie', 700, 1],
        // ['Podlaskie', 700, 3],
        // ['śląskie', 700, 5],
        // ['Swietokrzyskie', 700, 3],
        // ['Warminsko-Mazurskie', 700, 3],
        // ['Wielkopolskie', 700, 2],
        // ['Zachodniopomorskie', 700, 6],
        // ['Lubuskie', 700, 3],
      ],
      chartOptions: {
        region: 'PL',
        resolution: 'provinces',
        colorAxis: {
          colors: ['#FFCDD2', '#E57373', '#E53935'],
        },
        backgroundColor: { fill: '#FFEBEE' },
        legend: 'none',
      },
    };
  },

  methods: {
    getDataGChart() {
      this.loadingMap = true;
      fetch(this.secondUrl)
        .then((response) => {
          if (response.ok) {
            return response.json();
          }
        })
        .then((data) =>
          data.infectedByRegion.forEach((region) => {
            this.chartData.push([
              region.region.charAt(0).toUpperCase() + region.region.slice(1),
              region.infectedCount,
              region.deceasedCount,
            ]);
          })
        )
        .catch((error) => {
          console.log(error);
          this.loadingMap = true;
        });
      this.loadingMap = false;
      console.log(this.chartData);
    },
  },

  created() {
    this.getDataGChart();
  },
};
</script>

<style>
path {
  stroke: white;
  stroke-width: 1;
}

svg {
  border-radius: 0.5rem;
}
</style>
