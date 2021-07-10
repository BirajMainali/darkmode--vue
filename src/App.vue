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
<script>
export default {
  name: "App",
  data() {
    return {
      userTheme: "light-theme",
    };
  },
  methods: {
    setTheme(theme) {
      localStorage.setItem("user-theme", theme);
      this.userTheme = theme;
      document.documentElement.className = theme;
    },

    toggleTheme() {
      const activeTheme = localStorage.getItem("user-theme");
      if (activeTheme === "light-theme") {
        this.setTheme("dark-theme");
      } else {
        this.setTheme("light-theme");
      }
    },
    getMediaPreference() {
      const hasDarkPreference = window.matchMedia(
          "(prefers-color-scheme: dark)"
      ).matches;
      if (hasDarkPreference) {
        return "dark-theme";
      } else {
        return "light-theme";
      }
    },

  },
  mounted() {
    const initUserTheme = this.getMediaPreference();
    this.setTheme(initUserTheme);
  },

};
</script>

<style>
@import "../src/assets/style.css";
</style>
