<template>
  <v-app>
    <nav-bar></nav-bar>

    <v-container>
      <v-row>

        <card-info :loading=loadingCard1 titulo="Info 1" cuerpo="dato 1" color="primary"></card-info>
        <card-info :loading=loadingCard2 titulo="Info 2" cuerpo="dato 2" color="red"></card-info>
        <card-info :loading=loadingCard3 titulo="Info 3" cuerpo="dato 3" color="success"></card-info>
        <card-info :loading=loadingCard4 titulo="Info 4" cuerpo="dato 4"></card-info>

      </v-row>
    </v-container>


  </v-app>

</template>

<script setup>
const loadingCard1 = ref(true);
const loadingCard2 = ref(true);
const loadingCard3 = ref(true);
const loadingCard4 = ref(true);


definePageMeta({
  middleware: 'auth'
})
onMounted(() => {
  cargarCardDashboard1();
  cargarCardDashboard2();
  cargarCardDashboard3();
  cargarCardDashboard4();
})
const cargarCardDashboard1 = () => {

  setTimeout(() => {
    loadingCard1.value = false;
  }, 1500);

};
const cargarCardDashboard2 = () => {

  setTimeout(() => {
     loadingCard2.value = false;
  }, 1200);

};
const cargarCardDashboard3 = () => {

  setTimeout(() => {
    loadingCard3.value = false;
  }, 1800);

};
const cargarCardDashboard4 = () => {

  setTimeout(() => {
    loadingCard4.value = false;
  }, 500);

};

</script>