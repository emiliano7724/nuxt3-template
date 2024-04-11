<template>
  <v-card class="mx-auto">
    <v-card-title class="flex-column align-start">
      <v-row>
        <v-col cols="2">
          <v-avatar color="grey" rounded="1" size="100"
          >
            <v-img src="https://cdn.vuetifyjs.com/images/profiles/marcus.jpg" cover></v-img>
          </v-avatar>
        </v-col>
        <v-col cols="4">
          <div class="text-h4 mb-2">



          </div>
        </v-col>
        <v-col cols="6">

          <div class="data-item">
            <span class="label">Fecha de Nacimiento:</span>
            <v-chip size="x-large" color="indigo" prepend-icon="mdi-receipt" @click="lights">
              {{ fechaNacimiento }}
            </v-chip>
          </div>
          <div class="data-item">
            <span class="label">Unidad Regional:</span>
            <v-chip size="x-large" color="indigo" prepend-icon="mdi-receipt" @click="lights">
              {{ unidadRegional }}
            </v-chip>
          </div>

        </v-col>
      </v-row>

      <v-divider class="mx-10"></v-divider>

    </v-card-title>

  </v-card>

</template>

<script setup>


// Define las props
const props = defineProps({
  nombre: String,
  nroProntuario: String,
  fechaNacimiento: String,
  unidadRegional: String
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

