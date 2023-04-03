<script setup lang="ts">
  import { computed } from "@vue/reactivity";
  import axios from "axios"
  import {ref, watch} from "vue"
  const countries = ref()
  const input = ref()

  axios.get("https://restcountries.com/v3.1/all").then((res) => {
    countries.value = res.data
  })

  const filteredCountries = computed(() => {
    if(input.value !== "" && input.value && countries.value){
      return countries.value.filter(country => {
        return (country.name.common.toLowerCase()).includes(input.value)
      })
    }else{
      return countries.value
    }
  })

</script>

<template>
  <main>
    <div id="search">
      <p>Search</p>
      <input v-model="input" type="text" name="" id="" >
    </div>
    <div id="search-by-continent">

    </div>
    <div v-for="country in filteredCountries" class="country">
      <RouterLink :to="'/' + country.name.common">
        <div class="country-title">{{ country.name.common }}</div>
        <div class="country-flag"><img :src="country.flags.svg" :alt="country.name.common"></div>
      </RouterLink>
    </div>
  </main>
</template>


<style>
  #app{
    padding: 0;
    margin: 0;
    overflow-x: hidden;
  }
  main{
    width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    overflow-x: hidden;
    margin-top: 15px;
  }
  .country{
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 50%;
    margin: 25px 0px;
  }
  .country-title{
    font-size: 22px;
    font-weight: bold;
    margin-bottom: 15px;
  }
  .country-flag img{
    width: 100%;
    max-width: 500px;
  }
  a{
    text-decoration: none;
    color: white;
  }

  #search{
    display: flex; 
    gap: 15px;
  }
</style>