<template>
    <div>
      <table class="table table-bordered">
        <thead>
          <tr>
            <th scope="col" class="titulos">Título</th>
            <th scope="col" class="titulos">Calificación</th>
            <th scope="col" class="titulos">IMDB</th>
          </tr>
        </thead>
        <tbody>
          <tr v-if="pel.length === 0">
            <td colspan="3">No hay películas disponibles.</td>
          </tr>
          <tr v-for="pelicula in pel" :key="pelicula.id" @click="seleccionarPelicula(pelicula.movie)">
            <td class="fondo">{{ pelicula.movie }}</td>
            <td class="texto">{{ pelicula.rating }}</td>
            <td class="fondo">{{ pelicula.imdb_url }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    name: 'TablaPelis',
    props: {
      pel: {
        type: Array,
        required: true
      }
    },
    methods: {
      seleccionarPelicula(nombre) {
        this.$emit('pelicula-seleccionada', nombre); 
      }
    }
  }
  </script>
  
  <style scoped>
  table {
    cursor: pointer; 
  }
  
  .titulos {
    background-color: red;
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