<template>
  <v-card class="mx-auto" >
    <v-card-title class="flex-column align-start">
      <v-row justify="start">

        <v-col cols="4">

        {{ nombre }}

        <v-avatar color="grey" rounded="1" size="120">
          <v-img src="https://cdn.vuetifyjs.com/images/profiles/marcus.jpg" cover></v-img>
        </v-avatar>
        </v-col>
        <v-col>
        Prontuario N°:
        <v-chip size="x-large" color="indigo" prepend-icon="mdi-receipt" @click="lights">
          {{ nroProntuario }}
        </v-chip>
        </v-col>
        </v-row>
      <v-row>

        <v-col>

          Fecha nacimiento:
          <v-chip size="x-large" color="indigo" prepend-icon="mdi-receipt" @click="lights">
            {{ fechaNacimiento }}
          </v-chip>

        </v-col>
        <v-col  >

          Unidad Regional:
          <v-chip size="x-large" color="indigo" prepend-icon="mdi-receipt" @click="lights">
     UR I
          </v-chip>

        </v-col>
      </v-row>

    </v-card-title>

    <v-divider class="mx-4"></v-divider>

<!--    <v-card-text class="d-flex justify-space-between">
      <v-chip prepend-icon="mdi-brightness-5" @click="lights">Turn on lights</v-chip>
      <v-chip prepend-icon="mdi-alarm-check" @click="alarm">Set alarm</v-chip>
      <v-chip icon="mdi-blinds" @click="blinds">Close blinds</v-chip>
    </v-card-text>-->
  </v-card>
</template>

<script setup>


// Define las props
const props = defineProps({
  nombre: String,
  nroProntuario: String,
  fechaNacimiento: String
});

// Define los métodos
const alarm = () => {
  //alert('Turning on alarm...')
};
const blinds = () => {
  //alert('Toggling blinds...')
};
const lights = () => {
  //alert('Toggling lights...')
};
</script>
