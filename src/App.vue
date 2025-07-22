<script setup>
import { ref } from 'vue';
import CalculoNotas from './components/CalculoNotas.vue';
import FormularioRegistro from './components/FormularioRegistro.vue';

const vistaActual = ref('calculo');
</script>

<template>
  <div class="container py-4">
    <h1 class="text-center mb-4 text-primary"></h1>

    <!-- Navegación -->
    <ul class="nav nav-tabs mb-4">
      <li class="nav-item">
        <button
          class="nav-link"
          :class="{ active: vistaActual === 'calculo' }"
          @click="vistaActual = 'calculo'"
        >
          Cálculo de Calificaciones
        </button>
      </li>
      <li class="nav-item">
        <button
          class="nav-link"
          :class="{ active: vistaActual === 'formulario' }"
          @click="vistaActual = 'formulario'"
        >
          Formulario de Registro
        </button>
      </li>
    </ul>

    <!-- Vista dinámica -->
    <div>
      <CalculoNotas v-if="vistaActual === 'calculo'" />
      <FormularioRegistro v-else />
    </div>
  </div>
</template>



<style scoped>
.nav-link {
  cursor: pointer;
}
</style>
