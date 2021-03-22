<template>
  <nav>
    <v-navigation-drawer
      dark
      app
      mini-variant
      mini-variant-width="85"
      class="white"
    >
      <v-list dense nav>
        <v-list-item class="mb-12">
          <v-list-item-content>
            <v-icon color="red" class="my-3"> fas fa-virus</v-icon>
          </v-list-item-content>
        </v-list-item>

        <v-divider></v-divider>

        <v-list-item
          v-for="item in items"
          :key="item.title"
          router
          :to="item.route"
          class="mb-5"
          color="red"
        >
          <v-list-item-icon>
            <v-icon color="red">{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item style="position: absolute; bottom: 0" class="ma-5">
          <v-icon color="red">fas fa-sign-out-alt</v-icon>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { title: 'Dashboard', icon: 'fas fa-home', route: '/' },
        { title: 'About', icon: 'fas fa-columns' },
        { title: 'Chart', icon: 'fas fa-chart-line' },

        { title: 'FAQ', icon: 'far fa-question-circle' },
      ],
      right: null,
      mini: true,
      hover: false,
    };
  },
};
</script>
