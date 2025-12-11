<template>
  <Navbar />
  <router-view></router-view>
  <Footer />
</template>
<script setup>
import { RouterView } from 'vue-router'; // Yönlendirilmiş içeriği gösterir
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";

</script>
<style scoped lang="scss">
</style>
