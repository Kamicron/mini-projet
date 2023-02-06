<template>
  <button @click="toggleDarkMode">
    {{ darkMode ? "Light Mode" : "Dark Mode" }}
  </button>
</template>

<script>
export default {
  data() {
    return {
      darkMode: false
    };
  },
  methods: {
    toggleDarkMode() {
      this.darkMode = !this.darkMode;

      document.body.classList.toggle('dark-mode', this.darkMode);
    }
  }
};
</script>
