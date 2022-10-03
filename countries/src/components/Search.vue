<script setup lang="ts">
const props = defineProps(['filter']);

const search = (e: any) => {
  props.filter(e.target.value)
}
</script>


<template>
  <div class="container">
    <img src="@/assets/magnifying-glass-solid.svg" width="32" height="32" class="image" alt="search icon" />
    <input type="text" class="input" @keyup="search" placeholder="Search for a coutry..." />
  </div>
</template>

<style scoped>
@import url("@/assets/base.css");

.container {
  display: flex;
  align-content: flex-start;
}

.input {
  background-color: var(--color-background-secondary);
  padding: 25px;
  padding-left: 0;
  height: 75px;

  font-size: 1.2em;
  border: 0;
  color: var(--color-text);
  width: 500px;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;

}

.image {
  background-color: var(--color-background-secondary);
  height: 75px;
  width: 60px;
  padding: 15px;

  border-radius: 10px 0 0 10px;

}

.input::placeholder {
  color: var(--color-text);
  padding-left: 10px;
}

input:enabled {
  border: none;
  outline: none;
}

@media screen and (min-width:200px) and (max-width:900px) {
  .input {
    margin-bottom: 30px;
    width: 100%;
    padding: 0;
    text-align: start;
  }
}
</style>
