<template>
    <v-progress-linear
        v-if="cargando"
        color="purple"
        height="10"
        indeterminate
    ></v-progress-linear>

    <div>
        <img 
            v-if="!cargando && !error" 
            :src="imagenUrl" 
            style="border:5px solid red;" 
            @load="imagenCargada" 
            @error="imagenError" 
        >

        <div v-if="error" style="color: red; text-align: center;">
            <p>Error al cargar la imagen. Por favor, inténtalo de nuevo.</p>
        </div>

        <v-row justify="center" v-if="!cargando && !error">
            <v-col cols="auto">
                <v-btn
                    height="72"
                    min-width="164"
                    :disabled="loading"
                    @click="cambiarImagen"
                >
                    <template v-if="loading">Cargando...</template>
                    <template v-else>Cambiar imagen</template>
                </v-btn>
            </v-col>
        </v-row>
    </div>
</template>

<script setup>
import { ref } from "vue";

const imagenUrl = ref("https://picsum.photos/200/300");
const loading = ref(false);
const cargando = ref(true);
const error = ref(false);

function cambiarImagen() {
    if (loading.value) return;

    loading.value = true;
    cargando.value = true;
    error.value = false;

    const randomParam = Date.now();
    imagenUrl.value = `https://picsum.photos/200/300?random=${randomParam}`;
}

function imagenCargada() {
    loading.value = false;
    cargando.value = false;
}

function imagenError() {
    loading.value = false;
    cargando.value = false;
    error.value = true;
}

setTimeout(() => {
    cargando.value = false;
}, 3000);
</script>

<style scoped>
</style>