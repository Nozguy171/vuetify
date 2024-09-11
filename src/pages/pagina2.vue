<template>
  <v-container>
    <div class="text-center">
      <v-btn
        prepend-icon="mdi-arrow-left"
        @click="irRoot"
        class="borde"
      >
        <template v-slot:prepend>
          <v-icon color="warning"></v-icon>
        </template>
        Regresar a la página principal
      </v-btn>
    </div>

    <!-- Componente para mostrar el nombre de la película seleccionada -->
    <DetallePelicula :nombre="peliculaSeleccionada" />

    <TablaPelis :pel="pel" @pelicula-seleccionada="peliculaSeleccionada = $event" />

  </v-container>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRouter } from "vue-router";
import TablaPelis from "../components/tabla.vue";
import DetallePelicula from "../components/nombrePeli.vue"; // Importar el componente

const router = useRouter();
const pel = ref([]);
const peliculaSeleccionada = ref('');
const dialog = ref(false);

onMounted(async () => {
  try {
    const response = await fetch('https://dummyapi.online/api/movies');
    const peliculas = await response.json();
    pel.value = peliculas;
  } catch (error) {
    console.log(error);
  }
});

const irRoot = () => {
  router.replace("/");
};
</script>

<style>
.borde {
  border: 1px solid white;
}
</style>