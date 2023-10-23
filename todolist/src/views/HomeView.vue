<script setup>
import TheWelcome from "../components/TheWelcome.vue";
</script>

<template>
  <main>
    <TheWelcome />
    <nav>
      <RouterLink to="/">About</RouterLink>
      <RouterLink to="/today">Today</RouterLink>
    </nav>
  </main>
</template>
