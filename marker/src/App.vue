<template>
  <div :class="{ dark: isDarkMode }">
    <MarkdownEditor />
  </div>
</template>

<script lang="ts">
import { ref } from 'vue';
import MarkdownEditor from './components/MarkdownEditor.vue';

export default {
  components: { MarkdownEditor },
  setup() {
    const isDarkMode = ref(false);

    return {
      isDarkMode,
    };
  },
};
</script>

<style>
html,
body,
#app {
  height: 100%;
  margin: 0;
  padding: 0;
}

.dark {
  background-color: #111827;
  color: white;
}
</style>
