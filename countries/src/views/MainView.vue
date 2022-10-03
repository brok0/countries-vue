<script setup lang="ts">
import Country from '@/components/Country.vue';
import Search from '../components/Search.vue';
import Filter from '../components/Filter.vue';
import { ref, onMounted, reactive } from 'vue';

let countries = reactive([]);
const loading = ref(false);

const displayCountries = ref();

const filterCountries = (region: string) => {
  displayCountries.value = countries.filter((e: any) => e.region === region).slice(0, 20);
}

const filterBySearch = (search: string) => {
  if (search.trim() === '') {
    displayCountries.value = countries.slice(0, 20);
  }
  displayCountries.value = countries.filter((e: any) => { return e.name.official.toLowerCase().startsWith(search.toLowerCase()) }).slice(0, 20);

}

onMounted(async () => {
  const url = "https://restcountries.com/v3.1/all";
  loading.value = true;
  try {
    const result = await fetch(url);
    const json = await result.json();
    countries = json;
  } catch (err: any) {
    console.log(err);
  } finally {
    loading.value = false;
  }

  if (!displayCountries.value)
    displayCountries.value = countries.slice(0, 20);

})
</script>

<template>
  <main class="background">
    <div class="wrapper">
      <div class="inputs">
        <Search :filter="filterBySearch" />
        <Filter :filter="filterCountries" />
      </div>
      <p v-if="loading" class="loading">Loading countries...</p>
      <div class="card-container">
        <Country v-if="countries" v-for="country in displayCountries" :key="country.ccn3" :country="country"></Country>
      </div>
    </div>
  </main>
</template>


<style>
@import "@/assets/base.css";

.inputs {
  display: flex;
  justify-content: space-between;
  margin-bottom: 30px;
}

.card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 50px;

}

.background {
  padding-top: 50px;
  background-color: var(--color-background);
  color: var(--color-text);
}

.wrapper {
  margin-left: 100px;
  margin-right: 100px;
}

.loading {
  font-size: large;
}

@media screen and (min-width:700px) and (max-width:100px) {
  .card-container {
    flex-basis: 2;
  }
}

@media screen and (min-width:200px) and (max-width:700px) {
  .wrapper {
    margin-left: 10px;
    margin-right: 10px;
  }

  .inputs {
    display: block;
  }

  .background {
    padding-top: 25px;
  }

  .card-container {
    display: block;
    margin: 50px 40px;
  }

}
</style>
