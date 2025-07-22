<template>
  <div class="container mt-5">
    <div class="d-flex justify-content-center">
      <form @submit.prevent="validarFormulario" class="w-100" style="max-width: 500px;" novalidate>

        <!-- Nombre -->
        <div class="mb-3 text-center">
          <label class="form-label fw-bold text-center">Nombre:</label>
          <input type="text" class="form-control" v-model.trim="nombre" />
          <div v-if="errores.nombre" class="text-danger mt-1">{{ errores.nombre }}</div>
        </div>

        <!-- Correo -->
        <div class="mb-3 text-center">
          <label class="form-label fw-bold text-center">Correo:</label>
          <input type="email" class="form-control" v-model.trim="correo" />
          <div v-if="errores.correo" class="text-danger mt-1">{{ errores.correo }}</div>
        </div>

        <!-- Contraseña -->
        <div class="mb-3 text-center">
          <label class="form-label fw-bold text-center">Contraseña:</label>
          <input type="password" class="form-control" v-model="password" />
          <div v-if="errores.password" class="text-danger mt-1">{{ errores.password }}</div>
        </div>

        <!-- Repetir contraseña -->
        <div class="mb-3 text-center">
          <label class="form-label fw-bold">Repetir Contraseña:</label>
          <input type="password" class="form-control" v-model="confirmPassword" />
          <div v-if="errores.confirmPassword" class="text-danger mt-1">{{ errores.confirmPassword }}</div>
        </div>

        <!-- Botón -->
        <div class="text-start">
          <button type="submit" class="btn btn-success">Enviar</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const nombre = ref('');
const correo = ref('');
const password = ref('');
const confirmPassword = ref('');
const errores = ref({});

function validarFormulario() {
  errores.value = {};

  // Validar nombre
  if (!nombre.value) {
    errores.value.nombre = 'El campo nombre es requerido';
  }

  // Validar correo con expresión regular
  const regexCorreo = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!correo.value) {
    errores.value.correo = 'El campo correo es requerido';
  } else if (!regexCorreo.test(correo.value)) {
    errores.value.correo = 'El formato del correo no es válido';
  }

  // Validar contraseña
  if (!password.value) {
    errores.value.password = 'El campo contraseña es requerido';
  }

  // Validar repetir contraseña
  if (!confirmPassword.value) {
    errores.value.confirmPassword = 'El campo repetir contraseña es requerido';
  } else if (password.value && confirmPassword.value !== password.value) {
    errores.value.confirmPassword = 'Las contraseñas no coinciden';
  }

  // Si no hay errores
  if (Object.keys(errores.value).length === 0) {
    alert('El registro se ha realizado correctamente');
    
  }
}
</script>
