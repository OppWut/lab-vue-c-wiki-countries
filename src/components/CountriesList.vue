<template>
  <div class="container">
    <h1 v-if="!countries.length">Loading countries</h1>
    <div v-else class="row">        
      <div class="col-5" style="max-height: 90vh; overflow: scroll">
        <div class="list-group">
          <router-link v-for="(country, index) in countries" :key="index" class="list-group-item list-group-item-action d-flex flex-column justify-content-center align-items-center" :to="`/${country.alpha3Code}`">
            <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`" width="75" />
            <p class="m-0">{{ country.name.common }}</p>
          </router-link>
        </div>
      </div>
      <div class="col-7">
        <router-view />
      </div>
    </div>
  </div>  
</template>
<script>
export default {  
  data() {
    return {
      countries: [],      
    }
  },
  async mounted() {
    const response = await fetch("https://ih-countries-api.herokuapp.com/countries")
    const countries = await response.json()
    this.countries = countries
  }
}
</script>