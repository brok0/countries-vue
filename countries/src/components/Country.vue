<script setup lang="ts">
import { RouterLink } from 'vue-router';

const props = defineProps(['country']);
const capital = props.country?.capital[0] || "No capital";
</script>


<template>
  <router-link :to="{path:'/country',query:{name: props.country.name.official}}">
    <div class="card">
      <img :src="props.country.flags.png" class="image" :alt="props.country.name.official + '`s flag'" />
      <div class="text">
        <p class="country-name">{{props.country.name.official}}</p>
        <p><b>Population:</b> {{props.country.population}}</p>
        <p><b>Region:</b> {{props.country.region}}</p>

        <p><b>Capital:</b> {{capital}}</p>
      </div>
    </div>
  </router-link>
</template>

<style scoped>
@import "@/assets/base.css";

.card {
  border-radius: 15px;
  background-color: var(--color-background-secondary);
  width: 350px;
  height: 350px;
}

.image {
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
  width: 100%;
  height: 50%;
}

.text {
  padding: 20px;
}

.country-name {
  font-size: 18px;
  font-weight: 600;
  margin-bottom: 15px;
}

@media screen and (min-width:200px) and (max-width:900px) {
  .card {
    margin: auto;
    width: 100%;
    min-width: 200px;
    max-width: 350px;
    margin-bottom: 50px;
  }
}
</style>
