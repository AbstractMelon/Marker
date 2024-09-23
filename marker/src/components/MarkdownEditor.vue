<template>
    <div class="editor-wrapper h-screen flex flex-col">
      <Toolbar :isSplitScreen="isSplitScreen" @toggle-split-screen="toggleSplitScreen" @format-text="formatText" />
  
      <div v-if="isSplitScreen" class="flex-1 flex">
        <!-- Markdown Input Area -->
        <textarea
          v-model="markdownContent"
          class="w-1/2 p-4 dark:bg-gray-900 dark:text-gray-100 border-r border-gray-200 dark:border-gray-800"
          placeholder="Write your markdown here..."
        ></textarea>
  
        <!-- Preview Area -->
        <div
          class="w-1/2 p-4 dark:bg-gray-900 dark:text-gray-100"
          v-html="renderedMarkdown"
        ></div>
      </div>
  
      <div v-else class="flex-1">
        <!-- Combined Markdown Area -->
        <textarea
          v-model="markdownContent"
          class="w-full p-4 h-1/2 dark:bg-gray-900 dark:text-gray-100 border-b border-gray-200 dark:border-gray-800"
          placeholder="Write your markdown here..."
        ></textarea>
  
        <!-- Preview Area -->
        <div
          class="p-4 h-1/2 dark:bg-gray-900 dark:text-gray-100"
          v-html="renderedMarkdown"
        ></div>
      </div>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref, computed } from 'vue';
  import MarkdownIt from 'markdown-it';
  import Toolbar from './Toolbar.vue';
  
  export default defineComponent({
    components: { Toolbar },
    setup() {
      const markdownContent = ref('');
      const md = new MarkdownIt();
      const isSplitScreen = ref(true);
  
      const toggleSplitScreen = () => {
        isSplitScreen.value = !isSplitScreen.value;
      };
  
      const formatText = (formatType: string) => {
        let insertText = '';
        if (formatType === 'bold') {
          insertText = '**Bold Text**';
        } else if (formatType === 'italic') {
          insertText = '_Italic Text_';
        } else if (formatType === 'heading') {
          insertText = '# Heading';
        }
  
        markdownContent.value += insertText;
      };
  
      const renderedMarkdown = computed(() => md.render(markdownContent.value));
  
      return {
        markdownContent,
        renderedMarkdown,
        isSplitScreen,
        toggleSplitScreen,
        formatText,
      };
    },
  });
  </script>
  
  <style scoped>
  textarea {
    resize: none;
    width: 100%;
    height: 100%;
    outline: none;
    border: none;
    background-color: white;
    color: black;
  }
  
  .dark textarea {
    background-color: #1f2937;
    color: white;
  }
  </style>
  