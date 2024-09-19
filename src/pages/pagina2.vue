<template>
  <v-container>
    <h2 v-if="seleccionado"> Película Seleccionada: {{ seleccionado.movie }}</h2>

    <TablaPelis :peliculas="pel" @nombre_Pelicula2="peliculaSeleccionada" />
  </v-container>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRouter } from "vue-router";
import TablaPelis from "../components/tabla.vue";

const router = useRouter();
const pel = ref([]);
const seleccionado = ref(null);

function peliculaSeleccionada(payload) {
  seleccionado.value = payload;
}

onMounted(async () => {
  try {
    const response = await fetch('https://dummyapi.online/api/movies');
    const peliculas = await response.json();
    pel.value = peliculas;
  } catch (error) {
    console.log(error);
  }
});
</script>