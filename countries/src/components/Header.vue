<script setup lang="ts">
import { onMounted } from 'vue';
let userTheme = '';

function setTheme(theme: string) {
  localStorage.setItem("user-theme", theme);
  userTheme = theme;
  document.documentElement.className = theme;
}


function toggleTheme() {
  const activeTheme = localStorage.getItem("user-theme");
  if (activeTheme === "light-theme") {
    setTheme("dark-theme");
  } else {
    setTheme("light-theme");
  }
}

onMounted(() => {
  const activeTheme = localStorage.getItem("user-theme");

  setTheme(activeTheme);
})
</script>


<template>
  <header class="header">
    <div class="wrapper">
      <router-link to="/">
        <p class="logo">Where in the world?</p>
      </router-link>
      <div class="mode-toggle" @click="toggleTheme()">
        <img src="@/assets/moon-regular.svg" width="28" height="28" class="moon-icon" alt="moon icon" />
        <p class="toggle-text">Dark Mode</p>
      </div>
    </div>
  </header>

</template>

<style scoped>
@import url("@/assets/base.css");

.header {
  height: 100px;
  border-bottom: 3px solid rgba(175, 175, 175, 0.516);
  background-color: var(--color-background-secondary);
  display: block;
}

.logo {
  font-size: 1.4rem;
  font-weight: 600;

}

.wrapper {
  display: block;
  margin-left: 100px;
  margin-right: 100px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100%;

}

.mode-toggle {
  font-size: 1.2em;
  display: flex;
  align-items: center;

}

.moon-icon {
  margin-right: 15px;
}

.moon-icon svg path {
  color: var(--color-text);
}

@media screen and (min-width:200px) and (max-width:900px) {
  .header {
    display: block;
    width: 100vw;
  }

  .wrapper {
    margin-left: 10px;
    margin-right: 10px;
  }

  .logo {
    font-size: 1rem;
  }

  .mode-toggle {
    font-size: 0.8rem;
  }
}
</style>
