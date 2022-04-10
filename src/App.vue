<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from './components/HelloWorld.vue'
import Card from './components/Card.vue';
import TimeTracker from './components/TimeTracker.vue';
</script>

<template>
  <TimeTracker></TimeTracker>
</template>

<style lang="scss">
  @import "@/sass/style";

  #app {
    min-height: 100vh;
    background-color: $neutral-900;
    display: grid;
    align-items: center;
    justify-content: center;
    position: relative;
    z-index: 1;
    padding-top: 3rem;
    padding-bottom: 3rem;
  }
</style>
