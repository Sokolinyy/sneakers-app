<template>
  <router-view />

  <SneakerBox />
</template>

<script lang="ts" setup>
import SneakerBox from "./components/SneakerBox.vue";
</script>

<style lang="scss">
#app {
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: rgb(243, 243, 243);
}
</style>
