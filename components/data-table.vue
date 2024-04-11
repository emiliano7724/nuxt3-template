<template>
  <v-card
    title=""
    flat
  >
    <template v-slot:text>
      <v-text-field
        v-model="search"
        label="Buscar"
        prepend-inner-icon="mdi-magnify"
        variant="outlined"
        hide-details
        single-line
      ></v-text-field>
    </template>

    <v-data-table
      :headers="headers"
      :items="items"
      :search="search"
      no-data-text="No se encontraron datos"
    >
      <template v-slot:item.acciones="{ item }">
        <v-btn @click="verCardInfo(item)" color="primary" >
          Ver
        </v-btn>
        <v-btn  @click="verBookFotos(item)" variant="outlined" >
          Fotos
        </v-btn>
      </template>
    </v-data-table>

  </v-card>
</template>
<script setup>
const emit = defineEmits(['loading'])
 defineProps({
       items: Array ,
       headers: Array
 })
 const search=''
const verCardInfo = (item) => {

  emit('loading', true);

}






</script>