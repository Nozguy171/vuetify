<template>
  <div>
    <v-container>
      <v-progress-circular
        v-if="!cargado"
        :size="70"
        color="purple"
        indeterminate
      ></v-progress-circular>

      <div v-if="cargado && error" style="color: red; text-align: center;">
        <p>Error al cargar los datos. Por favor, inténtalo de nuevo.</p>
      </div>
      <v-container v-if="cargado && !error"> 
        <h2 v-if="seleccionado">Película Seleccionada: {{ seleccionado.movie }}</h2>

        <TablaPelis :peliculas="pel" @nombre_Pelicula2="peliculaSeleccionada" />
      </v-container>
    </v-container>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRouter } from "vue-router";
import TablaPelis from "../components/tabla.vue";

const router = useRouter();
const pel = ref([]);
const seleccionado = ref(null);
const cargado = ref(false); 
const error = ref(false);

function peliculaSeleccionada(payload) {
  seleccionado.value = payload;
}

onMounted(async () => {
  try {
    const response = await fetch('https://dummyapi.online/api/movies');
    if (!response.ok) {
      throw new Error('Error en la carga de datos');
    }
    const peliculas = await response.json();
    pel.value = peliculas;
  } catch (err) {
    console.error(err);
    setTimeout(() => {
      error.value = true; 
      cargado.value = true; 
    }, 3000); 
  } finally {
    setTimeout(() => {
      cargado.value = true;
    }, 3000);
  }
});
</script>

<style scoped>
</style>
