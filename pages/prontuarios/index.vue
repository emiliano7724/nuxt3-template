<template>
  <v-app>
    <nav-bar></nav-bar>
    <v-container>
      <v-row>

        <v-col cols="3">
          <v-card prepend-icon="mdi-account-alert" variant="outlined" :loading=false  title="Buscar persona">
            <v-card-actions>
              <v-col>
                <v-form>
                  <v-text-field
                      v-model="parametro"
                      :rules="rules"
                      label="N° prontuario o Nombre"
                  ></v-text-field>
                  <v-btn @click="buscar" color="blue" append-icon="mdi-account-search" block>Buscar</v-btn>
                </v-form>
              </v-col>
            </v-card-actions>
          </v-card>
        </v-col>

        <v-col cols="4">

          <v-card :loading=false elevation="16">
            <data-table title="Resultados" :items=items :headers=headers></data-table>

          </v-card>
        </v-col>


        <v-col cols="4">

          <v-card elevation="16" :loading=false title="Prontuario Seleccionado">
            <v-card-item>

              <v-card>
                <v-tabs
                    v-model=tab
                    bg-color=""
                >
                  <v-tab value="one">Datos Filiatorios</v-tab>
                  <v-tab value="two">Fotos</v-tab>

                </v-tabs>

                <v-card-text>
                  <v-window v-model=tab>
                    <v-window-item value="one">

                      <card-datos
                          :nombre=prontuario.nombre
                          :nroProntuario=prontuario.nroProntuario
                          :fechaNacimiento=prontuario.fechaNacimiento
                      >

                      </card-datos>
                    </v-window-item>

                    <v-window-item value="two">
                      <v-select
                          v-model="tipoIdentificacion"
                          label="Tipo"
                          :items="tiposIdentificacion"
                          variant="solo-inverted"
                          @change="updatePerfilOptions"
                      ></v-select>

                      <!-- Segundo v-select para Perfil -->
                      <v-select
                          v-model="perfil"
                          label="Perfil"
                          :items="perfilOptions"
                          variant="solo-inverted"
                      ></v-select>

                    </v-window-item>


                  </v-window>
                </v-card-text>
              </v-card>


            </v-card-item>
          </v-card>
        </v-col>


      </v-row>
    </v-container>

  </v-app>

</template>


  <script setup>

  definePageMeta({
    middleware: 'auth'
  });
  onMounted(() => {
    // Llamar a la función para que se ejecute al principio
    updatePerfilOptions();
  });

  const tipoIdentificacion = ref('Rostro');
  const perfil = ref('Derecho');

  // Define los tipos de identificación y perfiles
  const tiposIdentificacion = ['Rostro', 'Dactilar', 'Otro'];
  const perfilOptions = ['Derecho', 'Izquierdo', 'Frente'];

  // Función para actualizar las opciones del perfil según el tipo de identificación seleccionado
  const updatePerfilOptions = () => {

    if (tipoIdentificacion.value === 'Rostro') {
      perfilOptions.value = ['Derecho', 'Izquierdo', 'Frente'];
    } else if (tipoIdentificacion.value === 'Dactilar') {
      perfilOptions.value = ['Derecho', 'Izquierdo'];
    } else {
      perfilOptions.value = ['Tatuaje', 'Cicatriz', 'Otro'];
    }
  };


  const items = [];
  const prontuario = {
    nombre: "Emiliano Marquez",
    nroProntuario: "5564445",
    fechaNacimiento: "24/11/1988",
  };
  const rules = [
    value => {
      if (value) return true;
      return 'El campo es requerido';
    },
  ];
  const tab = ref('one');
  let parametro = '';

  // Opciones para la petición HTTP
  const options = {
    url: "http://httpbin.org/anything"
  };

  // Headers para la tabla
  const headers = [
    {
      align: 'start',
      key: 'nroProntuario',
      sortable: false,
      title: 'N° prontuario',
    },
    {key: 'nombre', title: 'Nombre'}
  ];

  // Función para buscar
  const buscar = () => {
    items.value = [
      // Puedes agregar objetos a 'items' según sea necesario
    ];
  };
</script>
