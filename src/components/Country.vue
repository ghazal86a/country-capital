<template>
  <div class="container">
    <h1>Random Country: {{ country }}</h1>
    <div class="form-group">
      <form>
        <label for="country">Capital City:</label>
        <input
          type="text"
          id="country"
          name="country"
          placeholder="Please enter the capital city"
          v-model="capital"
          required
        />
        <button type="submit" @click.prevent="OnSubmit()">
          Submit
        </button>
        <button type="submit" @click.prevent="TryAgain()">Try Again!</button>
      </form>
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
  },
  methods: {
    setRandomCountry(countries) {
      const randomCountry =
        countries[Math.floor(Math.random() * countries.length)].name;
      this.country = randomCountry;
    },
    OnSubmit() {
      const countryObj = this.allCountries.filter(
        country => country.name === this.country
      );
      const countryCapital = countryObj[0].capital;

      this.capital.toLowerCase() === countryCapital.toLowerCase() && this.capital !== ''
        ? (this.result = "Well Done!")
        : (this.result = `Sorry! The correct answer is: ${countryCapital}`);
    },
    TryAgain() {
      // reloads the page - better to use other methods e.g. forceUpdate,...
      // https://stackoverflow.com/questions/32106155/can-you-force-vue-js-to-reload-re-render
      this.$router.go(0);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
  background: #ffffff;
  width: 600px;
  border-radius: 10px;
  box-shadow: 0 0 30px rgba(#000000, 0.5);
  box-sizing: border-box;
  margin: 150px auto 10px;

  h1 {
    padding: 4px 0;
    color: #1b6930;
    font-size: 24px;
    font-weight: 700;
    text-transform: uppercase;
    text-align: center;
    word-wrap: break-word;
  }

  .form-group {
    padding: 10px;
    margin: 0 0 20px;
  }

  input {
    outline: none;
    display: block;
    background: rgba(#000000, 0.1);
    width: 100%;
    border: 0;
    border-radius: 4px;
    box-sizing: border-box;
    padding: 12px 20px;
    color: rgba(#000000, 0.5);
    font-family: inherit;
    font-size: inherit;
    font-weight: 500;
    line-height: inherit;
  }

  label {
    display: block;
    margin: 0 0 10px;
    color: rgba(#000000, 0.5);
    font-size: 12px;
    font-weight: 700;
    line-height: 1;
    text-transform: uppercase;
    letter-spacing: 0.2em;
  }

  button {
    outline: none;
    background: #1b6930;
    width: 100%;
    border: 0;
    margin-top: 8px;
    border-radius: 4px;
    padding: 12px 20px;
    color: #ffffff;
    font-family: inherit;
    font-size: inherit;
    font-weight: 500;
    line-height: inherit;
    text-transform: uppercase;
    cursor: pointer;
  }
}

@media screen and (max-width: 600px) {
  .container {
    width: 90%;
    margin: 50px auto;
  }
}
</style>
