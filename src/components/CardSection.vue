<template>
  <v-container>
    <v-carousel
      light
      :height="$vuetify.breakpoint.xs ? 560 : '280'"
      hide-delimiter-background
      show-arrows-on-hover
      class="rounded-lg"
    >
      <!---  #1-->
      <v-carousel-item v-for="(paragraph, i) in paragraphs" :key="i">
        <v-card height="100%" class="elevation-0 pa-5 mx-auto rounded-lg ">
          <v-row justify="center" class="fill-height" align="center">
            <v-col cols="12" sm="6">
              <h1
                v-html="h1[i]"
                class="text-h5 text-md-h4 font-weight-medium"
              ></h1>
              <p class="text-subtitle-2 text-md-subtitle-1 grey--text">
                {{ paragraph }}
              </p>
            </v-col>

            <v-col cols="12" sm="6">
              <v-img
                :class="{
                  'ma-auto': $vuetify.breakpoint.xs,
                  'ml-auto': $vuetify.breakpoint.smAndUp,
                }"
                max-width="50vh"
                :max-height="$vuetify.breakpoint.mdAndUp ? '18vh' : '16vh'"
                contain
                :src="imgSrc[i]"
                alt="Obraz przedstawiajcy COVID-19"
              />
            </v-col>
          </v-row>
        </v-card>
      </v-carousel-item>
    </v-carousel>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      h1: [
        'Czwarta szczepionka przeciw <span class="red--text">COVID-19</span> zatwierdzona.',
        'Zwiększamy możliwości testowania na <span class="red--text">COVID-19</span>',
        'W całej <span class="red--text">Polsce</span> obowiązują rozszerzone zasady bezpieczeństwa',
      ],
      paragraphs: [
        ' W maju do Polski mają dotrzeć pierwsze dostawy szczepionki Johnson & Johnson. Preparat tego producenta dostał „zielone światło” od Komisji Europejskiej.',
        ' Jeśli podejrzewasz u siebie Covid-19, nie czekaj! Wypełnij formularz online. Na podstawie przekazanych danych, dowiesz się, czy kwalifikujesz się na test.',
        'Sytuacja epidemiczna pogarsza się. Podjęliśmy decyzję o wprowadzeniu rozszerzonych zasad bezpieczeństwa w całej Polsce.',
      ],
      imgSrc: ['4.png', '5150374.jpg', '3724873.jpg'],
    };
  },
};
</script>

<style scoped></style>
