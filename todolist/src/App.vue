<script setup>
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";
import "./assets/main.css";
</script>

<template>
  <div class="app">
    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
    <div class="router">
     <RouterView />
    </div>
  </div>
</template>

<style scoped>
    .app{
      width: 100%;
      display: flex;
      
    }
    .wrapper{
      width: 20%;
    }
    .router{
      width: 70%;
      margin: 0 auto;
    }
</style>
