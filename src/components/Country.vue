<template>
  <div class="container">
    <h1>Random Country: {{ country }}</h1>
    <div class="form-group">
      <label for="country">Capital City:</label>
      <input
        type="text"
        id="country"
        name="country"
        placeholder="Please enter the capital city"
        v-model="capital"
        required
      />
      <button type="submit" @click="OnSubmit()">
        Submit
      </button>
      <h4>{{ result }}</h4>
    </div>
  </div>
</template>

<script>
export default {
  name: "Country",
  data() {
    return {
      allCountries: [],
      country: "",
      capital: "",
      result: ""
    };
  },
  async created() {
    // GET request using fetch with async/await
    const response = await fetch("https://restcountries.eu/rest/v2/all");
    const data = await response.json();
    this.allCountries = data;
    this.setRandomCountry(this.allCountries);
    console.log(this.allCountries);
  },
  methods: {
    setRandomCountry(countries) {
      const randomCountry =
        countries[Math.floor(Math.random() * countries.length)].name;
      this.country = randomCountry;
    },
    OnSubmit() {
      console.log("entered capital: ", this.capital);
      console.log(
        this.allCountries.filter(country => country.name === this.country)
      );
      const countryObj = this.allCountries.filter(
        country => country.name === this.country
      );
      const countryCapital = countryObj[0].capital;
      console.log("capital from object", countryCapital);

      this.capital.toLowerCase() === countryCapital.toLowerCase()
        ? (this.result = "Well Done!")
        : (this.result = `Sorry! The correct answer is: ${countryCapital}`);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
