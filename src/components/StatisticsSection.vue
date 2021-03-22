<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-chip
          label
          color="grey lighten-4"
          text-color="grey"
          class="text-center float-left"
        >
          <v-icon size="16" left>fas fa-exclamation-circle</v-icon>
          <p class="caption mb-0" :style="{ top: '50%', left: '50%' }">
            Ostatnia aktualizacja danych: {{ results.lastUpdate }}
          </p>
        </v-chip>
      </v-col>

      <v-col style="color: red" cols="12" sm="4">
        <v-card
          :class="{
            'mx-auto': $vuetify.breakpoint.xs,
            'mr-auto': $vuetify.breakpoint.smAndUp,
            'mt-2': true,
            'elevation-0': true,
            'rounded-lg': true,
          }"
          max-width="250"
        >
          <v-row class="pa-2 justify-space-between">
            <v-col cols="7">
              <v-list-item two-line>
                <v-list-item-content>
                  <v-list-item-subtitle color="grey" class="subtitle-2">
                    Zakażone
                    <v-icon color="red" class="mb-1">fas fa-caret-up</v-icon>
                  </v-list-item-subtitle>

                  <v-list-item-title>
                    <h3>
                      {{ results.confirmed | putComma }}
                    </h3>
                  </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-col>
            <v-col style="overflow: hidden" class="mr-3" cols="4">
              <v-sparkline
                class="ml-4 my-2"
                :fill="fill"
                padding="16"
                :value="value"
                :gradient="gradient"
                :smooth="radius || false"
                :line-width="width"
                :stroke-linecap="lineCap"
                :gradient-direction="gradientDirection"
                :type="type"
                :auto-line-width="autoLineWidth"
                auto-draw
              ></v-sparkline>
            </v-col>
          </v-row>
        </v-card>
      </v-col>

      <v-col cols="12" sm="4">
        <v-card class="elevation-0 mt-2 mx-auto  rounded-lg" max-width="250">
          <v-row class="pa-2 justify-space-between">
            <v-col cols="7">
              <v-list-item class="px-3" two-line>
                <v-list-item-content>
                  <v-list-item-subtitle color="grey" class="subtitle-2">
                    Wyzdrowiałe
                    <v-icon color="green" class=" mb-1">fas fa-caret-up</v-icon>
                  </v-list-item-subtitle>

                  <v-list-item-title>
                    <h3>{{ results.recovered | putComma }}</h3>
                  </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-col>
            <v-col style="overflow: hidden" class="mr-3" cols="4">
              <v-sparkline
                class="ml-4 my-2"
                :fill="fill"
                padding="16"
                :value="value2"
                :gradient="gradient2"
                :smooth="radius || false"
                :line-width="width"
                :stroke-linecap="lineCap"
                :gradient-direction="gradientDirection"
                :type="type"
                :auto-line-width="autoLineWidth"
                auto-draw
              ></v-sparkline>
            </v-col>
          </v-row>
        </v-card>
      </v-col>

      <v-col cols="12" sm="4">
        <v-card
          :class="{
            'mx-auto': $vuetify.breakpoint.xs,
            'ml-auto': $vuetify.breakpoint.smAndUp,
            'mt-2': true,
            'elevation-0': true,
            'rounded-lg': true,
          }"
          max-width="250"
        >
          <v-row class="pa-2 justify-space-between">
            <v-col cols="7">
              <v-list-item two-line>
                <v-list-item-content>
                  <v-list-item-subtitle color="grey" class="subtitle-2 ">
                    Zgony
                    <v-icon color="red" class="mb-1">fas fa-caret-up</v-icon>
                  </v-list-item-subtitle>

                  <v-list-item-title>
                    <h3>{{ results.deaths | putComma }}</h3>
                  </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-col>
            <v-col style="overflow: hidden" class="mr-3" cols="4">
              <v-sparkline
                class="ml-4 my-2"
                :fill="fill"
                padding="16"
                :value="value3"
                :gradient="gradient"
                :smooth="radius || false"
                :line-width="width"
                :stroke-linecap="lineCap"
                :gradient-direction="gradientDirection"
                :type="type"
                :auto-line-width="autoLineWidth"
                auto-draw
              ></v-sparkline>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import moment from 'moment';
const gradients = [
  ['#222'],
  ['#42b3f4'],
  ['green', 'green', '#f2fff4', 'white'],
  ['red', 'red', '#ffa6a6', 'white', 'white'],
  ['#00c6ff', '#F0F', '#FF0'],
  ['#f72047', '#ffd200', '#1feaea'],
];

export default {
  data() {
    return {
      url: 'https://covid19.mathdro.id/api/countries/Poland',
      results: {},
      width: 5,
      radius: 15,
      padding: 2,
      lineCap: 'round',
      gradient: gradients[3],
      gradient2: gradients[2],
      value: [0, 2, 5, 9, 5, 10, 3, 8, 5, 8, 5, 8, 2, 9, 0],
      value2: [5, 7, 0, 4, 3, 4, 10, 5, 2, 7, 9, 6, 5, 3, 5],
      value3: [0, 2, 5, 9, 5, 10, 3, 5, 2, 5, 2, 2, 2, 9, 0],
      gradientDirection: 'top',
      gradients,
      fill: true,
      type: 'trend',
      autoLineWidth: false,
    };
  },
  methods: {
    getData() {
      this.loading = true;
      console.log(`Loading: ${this.loading}`);
      fetch(this.url)
        .then((response) => {
          if (response.ok) {
            return response.json();
          }
        })
        .then((data) => {
          this.results = {
            confirmed: data.confirmed.value,
            recovered: data.recovered.value,
            deaths: data.deaths.value,
            lastUpdate: moment(data.lastUpdate)
              .locale('pl')
              .format('LLLL'),
          };

          console.log(this.results);
        })
        .catch((error) => {
          console.log(error);
          this.loading = true;
        });
      this.loading = false;
      console.log(`Loading: ${this.loading}`);
    },
  },
  filters: {
    putComma: (number) => {
      if (!number) return '';
      return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
    },
  },
  breakpoint: {
    thresholds: {},
  },
  created() {
    this.getData();
  },
};
</script>

<style>
svg.primary--text {
  transform: rotate(-45deg) scale(7);
}
</style>
