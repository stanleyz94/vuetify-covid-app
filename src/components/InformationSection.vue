<template>
  <v-container>
    <v-row>
     
      <v-col cols="12" md="6">
        <v-card class="rounded-lg " flat height="230">
          <v-row class="px-5">
            <v-col class="pa-3 " align-self="center" cols="4">
              <v-img max-width="250" max-height="180" src="3625643.jpg"></v-img>
            </v-col>
            <v-col cols="8" class="pa-3" align-self="start">
              <v-chip
                label
                :small="$vuetify.breakpoint.xs"
                class="ma-2 font-weight-bold pa-5"
                text-color="green "
                color="green lighten-5"
                >Zalecenia</v-chip
              >
              <v-card-text
                :class="{
                  'pa-2': true,
                  'font-weight-bold': true,
                  title: $vuetify.breakpoint.smAndUp ? true : false,
                }"
              >
                Masz koronawirusa lub podejrzewasz, że go masz?
              </v-card-text>
              <v-card-actions>
                <v-btn
                  :small="$vuetify.breakpoint.xs"
                  class="pl-0"
                  color="green"
                  text
                >
                  Zobacz więcej
                  <v-icon right>fa s fa-sign-out-alt</v-icon>
                </v-btn>
              </v-card-actions>
            </v-col>
          </v-row>
        </v-card>
      </v-col>

      <v-col cols="12" md="6">
        <v-card class="rounded-lg " flat height="230">
          <v-row class="px-5">
            <v-col class="pa-3 " align-self="center" cols="4">
              <v-img max-width="250" max-height="180" src="covid.jpg"></v-img>
            </v-col>
            <v-col cols="8" class="pa-3" align-self="start">
              <v-chip
                label
                :small="$vuetify.breakpoint.xs"
                class="ma-2 font-weight-bold pa-5"
                text-color="red accent-2"
                color="red lighten-5"
                >Ważne informacje</v-chip
              >
              <v-card-text
                :class="{
                  'pa-2': true,
                  'font-weight-bold': true,
                  title: $vuetify.breakpoint.smAndUp ? true : false,
                }"
              >
                Kolejne regiony objęte zasadami bezpieczeństwa
              </v-card-text>
              <v-card-actions>
                <v-btn
                  :small="$vuetify.breakpoint.xs"
                  class="pl-0"
                  color="red"
                  text
                >
                  Zobacz więcej
                  <v-icon right>fa s fa-sign-out-alt</v-icon>
                </v-btn>
              </v-card-actions>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {};
</script>
