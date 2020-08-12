<template>
  <div>
    <label for>Choose a Country</label>
    <select name="countries" id="countries" v-model="countryName">
      <option v-for="country in countries" :key="country" @input="getStates()">{{ country }}</option>
    </select>

    <p>{{ countryName }}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      countries: [],
      countryName: "",
      states: []
    };
  },
  mounted() {
    this.getCountries();
  },
  methods: {
    async getCountries() {
      axios
        .get(
          "http://allcountries.us-east-2.elasticbeanstalk.com/countries/list"
        )
        .then(result => {
          this.countries = result.data;
        });
    },
    getStates: function() {
      console.log("hi");
      axios
        .get(
          `http://allcountries.us-east-2.elasticbeanstalk.com/countries/details/${this.countryName}`
        )
        .then(result => {
          this.states = result.data;
          console.log(this.states);
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
