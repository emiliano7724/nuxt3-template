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
    ></v-data-table>
  </v-card>
</template>
<script>
  export default {
    props: {
      items: Array,
      headers: Array

    },
    data () {

      return {
        search: '',

      }
    },
  }
</script>