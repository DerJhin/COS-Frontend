<script setup>

import Header from "@/components/Header.vue";
</script>

<template>
  <v-layout>
    <Header/>
    <div class="d-flex text-center content">
      <router-view />
    </div>
  </v-layout>
</template>

<style scoped>
.content {
  margin-top: 85px;
  justify-content: center;
}

.v-layout {
  display: block;
}
</style>
