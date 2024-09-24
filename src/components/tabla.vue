<template>
  <div>
      <table class="table table-bordered">
          <thead>
              <tr>
                  <th scope="col" class="titulos">Título</th>
                  <th scope="col" class="titulos">Calificación</th>
                  <th scope="col" class="titulos">IMDB</th>
                  <th scope="col" class="titulos">Acciones</th>
              </tr>
          </thead>
          <tbody>
              <tr v-if="peliculas.length === 0">
                  <td colspan="4">No hay películas disponibles.</td>
              </tr>
              <tr v-for="pelicula in peliculas" :key="pelicula.id">
                  <td class="fondo" @click="nombre_Pelicula(pelicula)">{{ pelicula.movie }}</td>
                  <td class="fondo" style="cursor:default;">{{ pelicula.rating }}</td>
                  <td class="fondo" style="cursor:default;">
                      <a :href="pelicula.imdb_url" target="_blank">{{ pelicula.imdb_url }}</a>
                  </td>
                  <td class="fondo" style="cursor:default;">
                      <v-container>
                          <v-row align="center" justify="center">
                              <v-col cols="auto">
                                  <v-btn density="comfortable" icon="mdi-pencil" @click.stop.prevent="activarAjustes('edit', pelicula)"></v-btn>
                              </v-col>
                              <v-col cols="auto">
                                  <v-btn density="comfortable" icon="mdi-delete" @click.stop.prevent="activarAjustes('delete', pelicula)"></v-btn>
                              </v-col>
                          </v-row>
                      </v-container>
                  </td>
              </tr>
          </tbody>
      </table>

      <v-dialog v-model="dialogEdit" width="auto">
          <v-card max-width="800">
              <v-card-title>Editando película: {{ selectedMovie.movie }}</v-card-title>

              <v-card-text>¿Está seguro de que desea editar esta película? 
                  <v-col cols="12" md="auto" sm="6">
                      <v-text-field label= "Título" v-model="selectedMovie.movies"></v-text-field>
                  </v-col>
                  <v-col cols="12" md="auto" sm="6">
                      <v-text-field label= "Rating" v-model="selectedMovie.rating1"></v-text-field>
                  </v-col>
                  <v-col cols="12" md="auto" sm="6">
                      <v-text-field label= "IMDB URL" v-model="selectedMovie.imdb_url1"></v-text-field>
                  </v-col>
              </v-card-text>

              <template v-slot:actions>
                  <v-btn text @click="dialogEdit = false">Cancelar</v-btn>
                  <v-btn text @click="confirmEdit">Confirmar</v-btn>
              </template>
          </v-card>
      </v-dialog>

      <v-dialog v-model="dialogDelete" width="auto">
          <v-card max-width="800">
              <v-card-title>Eliminando película: {{ selectedMovie?.movie }}</v-card-title>
              <v-card-text>¿Está seguro de que desea eliminar esta película?</v-card-text>
              <template v-slot:actions>
                  <v-btn text @click="dialogDelete = false">Cancelar</v-btn>
                  <v-btn text @click.prevent="confirmDelete(selectedMovie)">Confirmar</v-btn> 
              </template>
          </v-card>
      </v-dialog>

  </div>

</template>

<script setup>
import { defineProps, defineEmits, ref } from 'vue';

const dialogEdit = ref(false);
const dialogDelete = ref(false);
const selectedMovie = ref(null);
let actualMovie = "";
const props = defineProps({
  peliculas: {
      type: Array,
      required: true,
  },
});

const emits = defineEmits(['nombre_Pelicula2']);

function nombre_Pelicula(pelicula) {
  const payload = {
      movie: pelicula.movie,
  };
  emits('nombre_Pelicula2', payload);
  actualMovie=payload.movie;
}

const activarAjustes = (action, pelicula) => {
  selectedMovie.value = pelicula; 
  selectedMovie.value.movies = selectedMovie.value.movie;
  selectedMovie.value.rating1 = selectedMovie.value.rating;
  selectedMovie.value.imdb_url1 = selectedMovie.value.imdb_url;
  if (action === 'edit') {
      dialogEdit.value = true; 
  } else if (action === 'delete') {
      dialogDelete.value = true; 
  }
};

const confirmEdit = () => {
  console.log(`Editando la película: ${selectedMovie.value.movie}`);
  
  if(selectedMovie.value.movies != null){
      selectedMovie.value.movie = selectedMovie.value.movies;
  }
  if(selectedMovie.value.imdb_url1 != null){
      selectedMovie.value.imdb_url = selectedMovie.value.imdb_url1;
  }
  if(selectedMovie.value.rating1 != null){
      selectedMovie.value.rating = selectedMovie.value.rating1;
  }
  
  nombre_Pelicula(selectedMovie.value);
  
  dialogEdit.value = false; 
};

const confirmDelete = (pelicula) => {
  if(actualMovie == pelicula.movie){
    nombre_Pelicula(" ");
    }
    props.peliculas.splice(props.peliculas.indexOf(pelicula), 1); 
    dialogDelete.value = false; 
};
</script>

<style scoped>
table {
  cursor: pointer; 
}

.titulos {
  background-color: blue;
  text-align: center;
  color: white;
}

.texto {
  text-align: right;
  background-color: black;
  color: white;
}

.fondo {
  background-color: black;
  color: white;
}
</style>
