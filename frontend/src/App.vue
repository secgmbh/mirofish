<template>
  <router-view />
</template>

<script setup>
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: 'JetBrains Mono', 'Space Grotesk', 'Noto Sans SC', monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #0F1B3D;
  background-color: #ffffff;
}

::-webkit-scrollbar { width: 8px; height: 8px; }
::-webkit-scrollbar-track { background: #EFF6FF; }
::-webkit-scrollbar-thumb { background: #2563EB; border-radius: 4px; }
::-webkit-scrollbar-thumb:hover { background: #1D4ED8; }

button { font-family: inherit; }
</style>
