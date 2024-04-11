<template>
<v-col cols="3">
<v-skeleton-loader v-if="loading" type="card">


</v-skeleton-loader>
  <v-card v-else
    elevation="16"
    :color=color
    variant="elevated"
    class="mx-auto"
    max-width="344"
    :title=titulo
    link
>
  <v-card-item>
    <div>
      <div class="text-overline mb-1">
     {{cuerpo}}
      </div>


    </div>
  </v-card-item>


</v-card>
</v-col>


</template>
<script setup>
defineProps(
    {
      titulo:String,
      cuerpo:String,
      color:String,
      loading:Boolean
    }

)



</script>