

<template>
  <v-app>
    <nav-bar></nav-bar>


    <v-card
        class="mb-1"
        density="compact"
        subtitle=""
        title="Dashboard"
        border
    >





    </v-card>


  </v-app>

</template>

<script setup>
definePageMeta({
  middleware: 'auth'
})
</script>