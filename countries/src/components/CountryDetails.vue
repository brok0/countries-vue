<script setup lang="ts">
import { ref } from 'vue';
import { useRoute, RouterLink } from 'vue-router';

const route = useRoute();
const countryName = ref(route.query.name);
const data: any = ref({});
const loading = ref(false);
const error = ref('');
const nameUrl = `https://restcountries.com/v3.1/name/${countryName.value}`;
const codeUrl = `https://restcountries.com/v3.1/alpha/${countryName.value}`;
let currency = "";
let officialName = "";

const getCountry = async () => {
  const url = countryName.value?.length === 3 ? codeUrl : nameUrl;
  loading.value = true;

  try {
    const response = await fetch(url);
    const json = await response.json();
    data.value = json[0];
  }
  catch (e) {
    error.value = e;
  }
  finally {
    loading.value = false;
    const firstKeyName = Object.keys(data.value.name.nativeName)[0];
    const firstKeyCurrency = Object.keys(data.value.currencies)[0];

    currency = data.value.currencies[firstKeyCurrency].name;
    officialName = data.value.name.nativeName[firstKeyName].official;
  }
}


await getCountry();


</script>


<template>
  <main class="main" :key="countryName">
    <p v-if="error">{{error}} while loading {{countryName}}</p>
    <router-link to="/" class="back-button"><img src="@/assets/arrow-left-solid.svg" width="32" height="32"
        alt="go back icon" />
      <p>Back</p>
    </router-link>

    <div v-if="data" class="container">

      <img :src="data.flags.png" class="image" :alt="data.name.official + '`s flag'" />
      <div class="info">
        <p class="country-name">{{data.name.official}}</p>

        <div class="country-details">

          <div class="country-details-main">
            <p>Native name: <span class="data">{{officialName}}</span> </p>
            <p>Population: <span class="data">{{data.population}}</span></p>
            <p>Region: <span class="data">{{data.region}}</span></p>
            <p>Sub Region: <span class="data">{{data.subregion}}</span> </p>
            <p>Capital: <span class="data">{{data.capital[0]}}</span></p>
          </div>
          <div class="country-details-secondary">
            <p>Top Level Domain: <span class="data">{{data.tld[0]}}</span></p>
            <p>Currencies: <span class="data">{{currency}}</span> </p>
            <p>Languages: <span v-for="lang in data.languages"><span class="data">{{lang +' '}}</span></span></p>
          </div>
        </div>

        <div class="borders-wrapper" v-if="data.borders">
          <p class="borders-label">Border countries:</p>
          <router-link v-for="cc in data.borders" :key="cc" :to="{path:'/country',query:{name:cc}}">
            <p class="borders"> {{cc}}</p>
          </router-link>
        </div>


      </div>

    </div>
  </main>
</template>

<style scoped>
@import url("@/assets/base.css");

.back-button {
  background-color: var(--color-background-secondary);
  display: flex;
  align-items: center;
  width: 130px;
  font-size: larger;
  justify-content: space-between;
  padding: 20px;
  margin: 30px;
  border-radius: 10px;
  margin-left: 100px;
}

.container {
  display: flex;

  margin-left: 100px;
  margin-right: 100px;
  height: 400px;
}

.info {
  margin-left: 30px;
  width: 100%;
}

.image {
  width: 40%;
  height: auto;
}

.country-name {
  font-size: 28px;
  font-weight: 600;
  margin-top: 50px;
  margin-bottom: 20px;
  margin-left: 12%;
}

.country-details {
  font-size: 16px;
  display: flex;
  width: 100%;
  justify-content: space-around;

}

span.data {
  opacity: 70%;
}

.country-details-main {}

.country-details-secondary {}

.borders {
  display: inline;
  background-color: var(--color-background-secondary);
  padding: 5px;
  padding-left: 20px;
  padding-right: 20px;
  border-radius: 10px;
  margin: 10px;
  opacity: 70%;
}

.borders-wrapper {
  display: flex;
  flex-wrap: wrap;
  margin-top: 25px;
  margin-bottom: auto;
  margin-left: 11%;
}

.main {
  width: 100vw;
}

.borders-label {
  display: inline;
}

@media screen and (min-width:200px) and (max-width:900px) {
  .container {
    display: block;
    margin-left: 10px;
    margin-right: 10px;
    height: auto;
  }

  .image {
    width: 100%;
  }

  .back-button {
    margin: 50px 10px;

  }

  .info {
    margin: 10px;
  }

  .country-details {
    display: block;
  }

  .country-name {
    margin: 30px 0;
  }

  .borders-wrapper {
    margin: 30px 0;
  }

  .country-details-main {
    margin-bottom: 30px;
  }

  .borders-label {
    margin-bottom: 30px;
  }
}
</style>
