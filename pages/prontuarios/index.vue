<template>
  <v-app>
    <nav-bar></nav-bar>
    <v-container>

      <v-row>

        <v-col cols="6">
          <v-card variant="outlined" prepend-icon="mdi-account-alert" elevation="16" :loading=false title="Buscar persona">
            <v-card-actions>
              <v-col cols="8">
                <v-form>
                  <v-text-field
                      v-model="parametro"
                      :rules="rules"
                      label="N° prontuario o Nombre"
                      variant="outlined"

                  ></v-text-field>
                </v-form>
              </v-col>
              <v-col cols="4">
                <v-btn
                    @click="buscar"
                    variant="tonal"
                    append-icon="mdi-account-search"
                    block
                    :loading=isSearchingProntuario>
                  Buscar
                </v-btn>
              </v-col>
            </v-card-actions>
          </v-card>
        </v-col>
        <v-col cols="6">
          <div v-if=isVisibleDataProntuario>
            <v-skeleton-loader
                v-if=loadingCardDatos
                type="card"
                :elevation="13"
            ></v-skeleton-loader>

            <v-card v-else elevation="16" :loading="false"
                    :title="'Prontuario Seleccionado: ' + prontuario.nro_prontuario">

              <v-card-item>

                <v-card-text>

                  <card-datos
                      :nombre=prontuario.nombre
                      :nroProntuario=prontuario.nro_prontuario
                      :fechaNacimiento=prontuario.fecha_nacimiento
                      :unidadRegional=prontuario.unidad_regional
                  >

                  </card-datos>
                  <v-expansion-panels>
                    <v-expansion-panel
                        title="Mas info"
                        text="Mas info por aca"
                    >
                    </v-expansion-panel>
                  </v-expansion-panels>


                </v-card-text>
                </v-card-item>
            </v-card>

          </div>
        </v-col>


      </v-row>

      <v-row>
        <v-col cols="6">


          <v-card v-if=isVisibleTabla :loading=isCargandoTabla elevation="16">
            <data-table
                title="Resultados"
                :items=items
                :headers=headers
                :isVisibleDataProntuario="isVisibleDataProntuario"
                @loading="toggleLoadingCardDatos">

            </data-table>

          </v-card>
        </v-col>

        <v-col cols="6">
          <div v-if=isVisibleDataProntuario>
            <v-skeleton-loader
                v-if=loadingCardDatos
                type="card"
                :elevation="13"
            ></v-skeleton-loader>

            <v-card v-else elevation="16" :loading="false"
                    title="Fotos">

              <v-card-item>

                <v-card>
                  <v-tabs
                      v-model=tab
                      bg-color=""
                  >

                    <v-tab value="one">Fotos Gestion</v-tab>
                    <v-tab value="two">Book Rostro</v-tab>
                    <v-tab value="three">Book Dactilar</v-tab>


                  </v-tabs>

                  <v-card-text>
                    <v-window v-model=tab>


                      <v-window-item value="one">
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

                      <v-window-item value="two">

                        <v-pagination></v-pagination>
                      </v-window-item>

                      <v-window-item value="three">

                        <v-pagination></v-pagination>
                      </v-window-item>
                    </v-window>
                  </v-card-text>
                </v-card>


              </v-card-item>
            </v-card>
          </div>
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

  updatePerfilOptions();
});

const loadingCardDatos = ref(false)
const isVisibleDataProntuario = ref(false);

const isCargandoTabla = ref(false);
const isVisibleTabla = ref(false);

const isSearchingProntuario = ref(false);


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


const items = ref([]);
/*  {
nombre: "Emiliano Marquez",
nro_prontuario: "5564445",
fecha_nacimiento: "24/11/1988",
unidad_regional: "UR I",
},
{
  nombre: "Nahuel Marquez",
  nro_prontuario: "87454",
  fecha_nacimiento: "24/11/1988",
  unidad_regional: "UR I",
}
] ;*/
const prontuario = {
  nombre: "Emiliano Marquez",
  nro_prontuario: "5564445",
  fecha_nacimiento: "24/11/1988",
  unidad_regional: "UR I",
};
const rules = [
  value => {
    if (value) return true;
    return 'El campo es requerido';
  },
];
const tab = ref('one');
let parametro = 'marquez';


// Headers para la tabla
const headers = [
  {
    align: 'start',
    key: 'nro_prontuario',
    sortable: true,
    title: 'N° prontuario',
  },
  {key: 'nombre', title: 'NOMBRE'},
  {key: 'fecha_nacimiento', title: 'FECHA NACIMIENTO', sortable: false,},
  {key: 'unidad_regional', title: 'UNIDAD REGIONAL', sortable: false,},
  {key: 'acciones', title: 'ACCIONES', sortable: false,}
];

// Función para buscar
const buscar = () => {
  isSearchingProntuario.value = true
  isCargandoTabla.value = true;

  // Simular una espera de 2 segundos antes de agregar los elementos
  setTimeout(() => {
    // Agregar elementos al arreglo items
    items.value.push({
          nombre: "Emiliano Marquez",
          nro_prontuario: "5564445",
          fecha_nacimiento: "24/11/1988",
          unidad_regional: "UR I",
        },
        {
          nombre: "Nahuel Marquez",
          nro_prontuario: "87454",
          fecha_nacimiento: "24/11/1988",
          unidad_regional: "UR I",
        }
    );

    isVisibleTabla.value = true;
    isSearchingProntuario.value = false;
    isCargandoTabla.value = false;
  }, 1500);

};
const toggleLoadingCardDatos = (value) => {
  isVisibleDataProntuario.value = true
  loadingCardDatos.value = value;
  setTimeout(() => {
    loadingCardDatos.value = !value;
  }, 1500);

};


</script>
