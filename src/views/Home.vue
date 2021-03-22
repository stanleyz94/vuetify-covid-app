<template>
  <div class="home">
    <header-section></header-section>
    <statistics-section></statistics-section>
    <card-section></card-section>

    <v-container>
      <v-row justify="space-between" class="fill-height">
        <v-col cols="12" md="6">
          <map-component></map-component>
        </v-col>
        <v-col align-self="center" cols="12" md="6">
          <chart-component></chart-component>
        </v-col>
      </v-row>
    </v-container>

    <information-section></information-section>
  </div>
</template>

<script>
import StatisticsSection from '../components/StatisticsSection.vue';
import ChartComponent from '../components/ChartComponent.vue';
import InformationSection from '../components/InformationSection.vue';
import CardSection from '../components/CardSection';
import MapComponent from '../components/MapComponent.vue';
import HeaderSection from '../components/HeaderSection.vue';

export default {
  components: {
    StatisticsSection,
    ChartComponent,
    InformationSection,
    CardSection,
    MapComponent,
    HeaderSection,
  },
  data() {
    return {};
  },

  methods: {},
};
</script>

<style></style>
