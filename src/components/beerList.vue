<template>
  <v-container>
    <v-card>
      <v-card-title>
        <h4 class="purple pa-2">BeerDB</h4>
        <v-spacer></v-spacer>
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          single-line
          hide-details
        ></v-text-field>
      </v-card-title>
      <v-data-table
        :headers="headers"
        :items="beers"
        :search="search"
        :itemsPerPage="20"
        item-key="name"
        :footer-props="{
            disableItemsPerPage: true,
        }"
      ></v-data-table>
    </v-card>
  </v-container>
</template>
<style type="css" scoped>
    .v-data-footer__select{
        display: none;
    }
</style>
<script>
export default {
  name: "BeerList",
  data() {
    return {
      images:[],
      beers: [],
      search: "",
      headers: [
        {
          text: "Beer Name",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "Style", value: "style" },
        { text: "IBU", value: "ibu" },
        { text: "ABV", value: "abv" },
        { text: "Ounces", value: "ounces" },
      ],

    };
  },
  methods: {},
  created() {
    fetch(
      "https://s3-ap-southeast-1.amazonaws.com/he-public-data/beercraft5bac38c.json"
    ).then((response) => {
      // Examine the text in the response
      response.json().then((data) => {
        data.forEach((beer) => {
          const dat = {
            abv: beer.abv,
            ibu: beer.ibu,
            id: beer.id,
            name: beer.name,
            style: beer.style,
            ounces: beer.ounces,
            image_url: null
          };
          this.beers.push(dat);
        });
      });
    });
    fetch("https://s3-ap-southeast-1.amazonaws.com/he-public-data/beerimages7e0480d.json").then((response)=>{
        response.json().then((data)=>{
            data.forEach((img)=>{
                const data={
                    imag_url: img.image
                }
                this.images.push(data);
            })
        })
    });
    
    if(this.beers.length){
        this.beers.forEach((beer)=>{
            this.images.forEach((img)=>{
                beer.push(img);
            })
        })
    }
  },
};
</script>
