<template>

    <v-app-bar

        :elevation="16"


    >
      <v-img
          :width="273"
          aspect-ratio="16/9"
          cover
          src="https://cdn.vuetifyjs.com/images/parallax/material.jpg"
      ></v-img>

      <template v-slot:image>

      </template>
      <v-toolbar-title>Consulta Prontuario</v-toolbar-title>
      <v-spacer></v-spacer>

      <v-btn text  @click="goToDashboard()">
        <v-icon>mdi-view-dashboard</v-icon>
        Dashboard
      </v-btn>

      <v-btn text  @click="goToConsultar()">
        <v-icon>mdi-account-search</v-icon>
        Prontuarios
      </v-btn>

      <v-btn text  @click="logout()">
        <v-icon>mdi-exit-to-app</v-icon>
        Salir
      </v-btn>
      <!-- Puedes agregar más elementos de la barra de navegación según sea necesario -->
    </v-app-bar>


  <br><br><br><br>

</template>

<script>
import {navigateTo} from "nuxt/app";

export default {
  data() {
    return {
      isMenuOpen: false
    }
  },
  methods: {
    toggleMenu(item) {
      // Cambiar el estado de visibilidad del menú
      this.isMenuOpen = !this.isMenuOpen;

      // Puedes agregar lógica adicional para manejar acciones específicas para cada ítem si es necesario
      console.log('Hizo clic en:', item);
    },
    goToConsultar(){
      navigateTo("/prontuarios")
    },
    goToDashboard(){
      navigateTo("/dashboard")
    },
    logout(){
      navigateTo("/")
    }
  }
}
</script>

<style>
/* Estilos personalizados si es necesario */
</style>
