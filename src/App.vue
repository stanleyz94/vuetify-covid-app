<template>
  <v-app>
    <NavigationSection />
    <v-main class="mx-5 mb-4 grey lighten-4">
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
import NavigationSection from './components/NavigationSection.vue';

export default {
  components: {
    NavigationSection,
  },
};
</script>

<style>
#app > div > main {
  padding: 0 !important;
}
</style>
