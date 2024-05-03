<template>
  <div class="wrapper">
    <GameHilo></GameHilo>
  </div>
</template>

<script lang="ts" setup>
import GameHilo from "@/components/GameHilo.vue";
</script>

<style lang="scss">
.wrapper {
  width: 100%;
  height: 100vh;
}
body {
  margin: 0;
}
</style>
