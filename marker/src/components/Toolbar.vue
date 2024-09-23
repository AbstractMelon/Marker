<template>
    <div class="flex items-center p-2 bg-gray-200 dark:bg-gray-800 border-b dark:border-gray-700">
      <button @click="formatText('bold')" class="toolbar-btn">B</button>
      <button @click="formatText('italic')" class="toolbar-btn">I</button>
      <button @click="formatText('heading')" class="toolbar-btn">H</button>
      <button @click="toggleSplitScreen" class="toolbar-btn">
        {{ isSplitScreen ? 'Single' : 'Split' }}
      </button>
      <DarkModeToggle class="ml-auto" />
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent } from 'vue';
  import DarkModeToggle from './DarkModeToggle.vue';
  
  export default defineComponent({
    components: { DarkModeToggle },
    props: {
      isSplitScreen: {
        type: Boolean,
        required: true,
      },
      toggleSplitScreen: {
        type: Function,
        required: true,
      },
    },
    setup(_, { emit }) {
      const formatText = (formatType: string) => {
        emit('format-text', formatType);
      };
  
      return {
        formatText,
      };
    },
  });
  </script>
  
  <style scoped>
  .toolbar-btn {
    padding: 0.5rem 1rem;
    margin-right: 0.5rem;
    border: none;
    background-color: transparent;
    cursor: pointer;
    font-weight: bold;
  }
  
  .toolbar-btn:hover {
    background-color: #f0f0f0;
  }
  
  .dark .toolbar-btn:hover {
    background-color: #3b3b3b;
  }
  </style>
  