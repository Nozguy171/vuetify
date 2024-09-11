<template>
    <div class="text-center">
    <v-btn
      prepend-icon="mdi-arrow-right"
      @click = "irTabla()"
      class = "borde"
    >
      <template v-slot:prepend>
        <v-icon color="success"></v-icon>
      </template>
      Ir a la pagina de la tabla
    </v-btn>
  </div>
<HelloWorld />
</template>

<script setup>
import {ref} from "vue";
import router from "../router";
const show = ref(false);
function irTabla(){
    router.replace("/pagina2");
}
  //
</script>
