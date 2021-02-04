<template>
  <div>
    <h1>Liste des constructeur F1</h1>
    <ul>
      <p>écurie:</p>
      <li v-for="ecuri in rakingArray" :key="ecuri.team_name">
        {{ ecuri.team_name }}
      </li>
    </ul>
    <button @click="Raking">essai</button>
    <b-input placeholder="saisir une année" v-model="year"></b-input>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      year: "",
      rakingArray: "",
      url: `https://f1-live-motorsport-data.p.rapidapi.com/constructors/`,
      config: {
        headers: {
          "x-rapidapi-key":
            "057047dc3fmsh9707bb7fe250977p1cecf7jsne21272259745",
          "x-rapidapi-host": "f1-live-motorsport-data.p.rapidapi.com",
        },
      },
    };
  },
  methods: {
    getF1Raking() {
      axios
        .get(this.url + this.year, this.config)
        .then((response) => (this.rakingArray = response.data.results))
        .catch(function(error) {
          console.error(error);
        });
    },
    async Raking() {
      this.rakingArray = await this.getF1Raking();
    },
  },
};
</script>

<style lang="scss" scoped></style>
