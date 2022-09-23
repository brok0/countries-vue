<script setup lang="ts">
import { ref } from 'vue';
const options = ['Africa', 'Americas', 'Asia', 'Europe', 'Oceania'];
const props = defineProps({
  filter: Function,
})
const selectedOption = ref('');

const setOption = (e) => {
  selectedOption.value = e.target.value;
  props.filter(selectedOption.value);
}


</script>


<template>
  <div>
    <select type="select" class="input" @change="setOption">
      <option value="" disabled selected>Filter by region</option>
      <option v-for="option in options" :value="option" class="option">
        {{option}}
      </option>
    </select>
  </div>
</template>

<style scoped>
@import url("@/assets/base.css");

.input {
  background-color: var(--color-background-secondary);
  padding: 25px;
  font-size: 1.2em;
  border: 0;
  color: var(--color-text);
  width: 200px;
  border-radius: 10px;


}

select {
  background: url(http://cdn1.iconfinder.com/data/icons/cc_mono_icon_set/blacks/16x16/br_down.png) no-repeat right white;
  -webkit-appearance: none;
  background-position-x: 160px;
  color: var(--color-text);
}

select:enabled {
  border: none;
  outline: none;
}

.option {
  margin-left: 5px;
  margin-bottom: 10px;
}
</style>
