<template>  
  <div v-if="country.alpha3Code">
    <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`" alt="country flag" style="width: 200px" />
    <h1>{{ country.name.common }}</h1>
    <table class="table">
      <thead></thead>
      <tbody>
        <tr>
          <td style="width: 30%">Capital</td>
          <td>{{ country.capital[0] }}</td>
        </tr>
        <tr>
          <td>Area</td>
          <td>{{ country.area }} km <sup>2</sup></td>
        </tr>
        <tr v-if="country.borders.length > 0">
          <td>Borders</td>
          <td>
            <ul class="list-style-none">
              <li v-for="(borderAlpha3Code, index) in country.borders" :key="index">
                <router-link :to="`/${borderAlpha3Code}`">
                  {{ borderAlpha3Code }}
                </router-link>
              </li>
            </ul>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        country: {},
      };
    },    
    watch: {
      '$route.params.alpha3Code': {
        async handler() {
          if (this.$route.params.alpha3Code) {
            const response = await fetch(`https://ih-countries-api.herokuapp.com/countries/${this.$route.params.alpha3Code.toUpperCase()}`);
            const country = await response.json();
            this.country = country;
          }
        },
        immediate: true
      }
    }
  };
</script>
<style></style>