<template>
<v-app>
  <v-container>
    <v-card
        class="mx-auto"
        max-width="400"
    >
      <v-img
          class="align-end text-white"
          height="200"
          src="https://cdn.vuetifyjs.com/images/cards/house.jpg"
          cover
      >
        <v-card-title>Iniciar sesión</v-card-title>
      </v-img>

      <v-card-text>
        <v-form @submit.prevent="login">
          <v-text-field
              v-model="email"
              label="Email"
              required
          ></v-text-field>

          <v-text-field
              v-model="password"
              label="Contraseña"
              type="password"
              required
          ></v-text-field>
        </v-form>
      </v-card-text>

      <v-card-actions>
        <v-btn
            color="primary"
            block
            @click="login"
        >
          Iniciar sesión
        </v-btn>
      </v-card-actions>
    </v-card>


  </v-container>

</v-app>

</template>

<script>
import {navigateTo} from "nuxt/app";

export default {
  data() {
    return {
      email: 'admin@admin.com',
      password: '1q2w3e4r'
    }
  },
  methods: {
    login() {
      navigateTo("/dashboard")
    }
  }
}
</script>
