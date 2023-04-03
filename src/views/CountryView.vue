<script setup lang="ts">
  import axios from "axios"
  import {ref} from "vue"
  import router from "../router/index"
  const countryData = ref()

  axios.get(`https://restcountries.com/v3.1/name/${router.currentRoute.value.params.name}`).then((res) => {
      countryData.value = res.data
      console.log(res)
  })
    
</script>

<template>
  <main>
    <div id="country">
        <div class="country-name">
            <h1>{{ countryData[0].name.common }}</h1>
        </div>
        <div class="country-flag">
            <img :src="countryData[0].flags.svg" :alt="countryData[0].name.common">
        </div>
        <div class="capital-container">
            <p>Capital : </p>
            <p v-for="capital in countryData[0].capital">
                {{ capital }}
            </p>
        </div>
        <div class="population-container">
            <p>Nombre d'habitant : </p>
            <p>{{ countryData[0].population }}</p>
        </div>
        <div class="area">
            <p>Superficie</p>
            <p>{{ countryData[0].area }}</p>
        </div>
        <div class="language-container">
            <p>Langages</p>
            <p v-for="language in countryData[0].languages">{{ language }}</p>
        </div>
    </div>
  </main>
</template>


<style>
  body{
    min-height: none !important;
  }
  #app{
    padding: 0;
    margin: 0;
    overflow-x: hidden;
  }

  #country{
    font-size: 22px;
    display: flex;
    flex-direction: column;
    gap: 15px;
  }

  div p:first-of-type{
    font-size: 24px;
    font-weight: bold;
  }

</style>