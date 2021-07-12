<template>
  <div class="container-center">
    <div class="card">
      <input
          @change="toggleTheme"
          id="checkbox"
          type="checkbox"
          class="switch-checkbox"
      />
      <label for="checkbox" class="switch-label">
        <span>🌙</span>
        <span>☀️</span>
        <div
            class="switch-toggle"
            :class="{ 'switch-toggle-checked': userTheme === 'dark-theme' }"
        ></div>
      </label>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aut dicta dolorum in ipsa mollitia nemo nihil
        possimus quis quisquam voluptatem. Aspernatur est ex labore, necessitatibus officia suscipit unde. Alias,
        officia.
      </p>
    </div>
  </div>
</template>
<script setup>
import {onMounted, ref} from "vue";

const userTheme = ref("light-theme")

const setTheme = (theme) => {
  localStorage.setItem("user-theme", theme);
  userTheme.value = theme
  document.documentElement.className = theme;
}

const toggleTheme = () => {
  const activeTheme = localStorage.getItem("user-theme");
  if (activeTheme === "light-theme") {
    setTheme("dark-theme")
  } else {
    setTheme("light-theme")
  }
}
const getMediaPreference = () => {
  const hasDarkPreference = window.matchMedia("(prefers-color-scheme: dark)").matches;
  if (hasDarkPreference) {
    return "dark-theme";
  } else {
    return "light-theme";
  }
}

onMounted(() => {
  const currentTheme = localStorage.getItem('user-theme');
  if (currentTheme !== null) {
    setTheme(currentTheme);
  } else {
    const initUserTheme = getMediaPreference();
    setTheme(initUserTheme);
  }
})

</script>

<style>
@import "../src/assets/style.css";
</style>
