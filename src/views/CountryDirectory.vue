<template>
  <div>
    <div class="forms">
      <div>
        <label>Choose a Country</label>
        <div class="box">
          <select
            name="countries"
            id="countries"
            v-model="countryName"
            @change="countryPick($event)"
          >
            <option
              :value="country.name"
              v-for="country in countries"
              :key="country.id"
            >{{ country.name }}</option>
          </select>
        </div>
        <div class="box">
          <label>Choose a State</label>
          <select name="state" id="state" v-model="stateName" @change="statePick($event)">
            <option :value="state.name" v-for="state in states" :key="state.id">{{ state.name }}</option>
          </select>
          <div v-if="noState" class="error">No states here!</div>
        </div>
        <div class="box">
          <label>Choose a City</label>
          <select name="city" id="city" v-model="cityName">
            <option :value="city.name" v-for="city in cities" :key="city.id">{{ city.name }}</option>
          </select>
          <div v-if="noCity" class="error">No city here!</div>
        </div>
        <button @click="clear()">Clear</button>
      </div>
      <div class="details">
        <p>
          Country:
          <span>{{ countryName }}</span>
        </p>
        <p>
          State:
          <span>{{ stateName }}</span>
        </p>
        <p>
          City:
          <span>{{ cityName }}</span>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
// import axios from "axios";
export default {
  data() {
    return {
      countryName: "",
      stateName: "",
      cityName: "",
      countries: [],
      states: [],
      cities: [],
      noState: "",
      noCity: ""
    };
  },
  mounted() {
    fetch(
      "https://raw.githubusercontent.com/dr5hn/countries-states-cities-database/master/countries%2Bstates%2Bcities.json"
    )
      .then(response => {
        return response.json();
      })
      .then(data => {
        this.countries = data.slice(0, 500);
      });
  },
  methods: {
    clear() {
      if (this.countryName && this.stateName && this.cityName !== "") {
        this.countryName = "";
        this.stateName = "";
        this.cityName = "";
      }
    },
    countryPick(event) {
      const state = event.target.value;
      const index = this.countries.findIndex(x => x.name === state);
      const countryHasState = this.countries[index]["states"];
      if (countryHasState.length === 0) {
        this.noState = !this.noState;
        this.states = null;
        this.cities = "";
      } else {
        this.states = countryHasState;
        this.noState = false;
      }
    },
    statePick(event) {
      const state = event.target.value;
      const index = this.states.findIndex(x => x.name === state);
      const city = this.states[index]["cities"];
      if (city.length === 0) {
        this.noCity = !this.noCity;
      } else {
        this.cities = city;
        this.cityEmptyError = false;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.box {
  display: inline;
  margin: auto 1rem;
}

.forms {
  position: relative;
  bottom: 2rem;
  left: 10.5rem;
  background: beige;
  display: flex;
  align-items: center;
  padding: 5rem 14rem;
  background-size: inherit;
  justify-content: space-between;
  width: 33rem;
  height: 23rem;
}

label {
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  color: rgb(76, 133, 184);
}
.details {
  flex: 0 0 50%;

  margin: 0 3rem;
}
.details p {
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  color: rgb(76, 133, 184);
  margin: 2rem 0;
}
.details p span {
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  color: rgb(76, 133, 184);
  font-size: 1rem;
}
select {
  height: 2rem;
  width: 18rem;
  border: 1px solid green;
  padding: 1rem 1rem;
  border-radius: 3px;
  margin: 2rem 0;
  display: block;
  background-color: rgb(244, 245, 201);
  color: black;
}
.error {
  margin: 2rem 0;
}
button {
  height: 3rem;
  width: 5rem;
  background-color: blue;
  color: white;
  border: 1px solid transparent;
  border-radius: 3px;
}
</style>
