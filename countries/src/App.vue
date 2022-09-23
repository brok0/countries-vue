<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import Header from './components/Header.vue'
</script>

<template>
  <Header></Header>
  <RouterView v-slot="{Component}" :key="$route.params">

    <Suspense>
      <component :is="Component" />
    </Suspense>

  </RouterView>
</template>

<style scoped>

</style>
