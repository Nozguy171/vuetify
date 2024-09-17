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
    <h2 v-if="seleccionado"> Película Seleccionada: {{ seleccionado.movie }}</h2>

    <!-- Asegúrate de pasar 'pel' como 'peliculas' -->
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
  seleccionado.value = payload; // Cambié 'payload' por 'pelicula'
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

const irRoot = () => {
  router.replace("/");
};
</script>

<style>
.borde {
  border: 1px solid white;
}
</style>