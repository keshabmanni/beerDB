<template>
  <v-app>
    
    <v-main>
      <BeerList />
    </v-main>
  </v-app>
</template>

<script>
import BeerList from "./components/beerList.vue";

export default {
  name: "App",

  components: {
    BeerList,
  },

  data: () => ({
    //
  }),
};
</script>
