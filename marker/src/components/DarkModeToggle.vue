<template>
    <button @click="toggleDarkMode" class="p-2 bg-gray-200 dark:bg-gray-700 text-black dark:text-white">
      {{ isDarkMode ? 'Light Mode' : 'Dark Mode' }}
    </button>
  </template>
  
  <script lang="ts">
  import { ref } from 'vue';
  
  export default {
    setup() {
      const isDarkMode = ref(false);
  
      const toggleDarkMode = () => {
        isDarkMode.value = !isDarkMode.value;
        document.documentElement.classList.toggle('dark', isDarkMode.value);
      };
  
      return {
        isDarkMode,
        toggleDarkMode,
      };
    },
  };
  </script>
  