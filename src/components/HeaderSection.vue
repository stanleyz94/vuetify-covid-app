<template>
  <header>
    <v-container>
      <v-row no-gutters>
        <v-col cols="12" sm="6">
          <v-text-field
            class="mt-2"
            placeholder="Szukaj"
            append-icon="mdi-magnify"
            filled
            dense
            solo
            flat
            background-color="white"
            color="red"
          ></v-text-field>
        </v-col>

        <v-col cols="12" sm="6" class="text-center">
          <v-chip
            height="170"
            label
            color="grey lighten-4"
            text-color="grey"
            class="pa-6 float-md-right"
          >
            <v-badge
              offset-x="16"
              offset-y="16"
              class="mr-2"
              color="red"
              content="2"
            >
              <v-btn icon>
                <v-icon color="grey" size="27">
                  far fa-bell
                </v-icon>
              </v-btn>
            </v-badge>
            <v-btn class="mr-2" icon>
              <v-icon size="27" color="grey">fas fa-ellipsis-v</v-icon>
            </v-btn>
            <v-badge offset-x="7" offset-y="7" bottom dot color="green">
              <v-img
                width="38"
                height="38"
                class="rounded-lg"
                src="avatar.jpg"
              ></v-img>
            </v-badge>
          </v-chip>
        </v-col>
      </v-row>
    </v-container>
  </header>
</template>

<script>
export default {};
</script>
