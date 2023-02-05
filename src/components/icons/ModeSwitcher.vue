<template>
  <div>
    <button @click="toggleDarkMode">
      <template v-if="darkMode">Light Mode</template>
      <template v-else>Dark Mode</template>
    </button>
  </div>
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
    }
  }
};
</script>