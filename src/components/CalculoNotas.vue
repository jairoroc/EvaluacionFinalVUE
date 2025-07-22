<template>
  <div class="container mt-5">
    <div class="d-flex justify-content-center">
      <form @submit.prevent="calcularPromedio" class="w-100" style="max-width: 500px;" novalidate>
        
        <!-- Nota 1 -->
        <div class="mb-3 text-center">
          <label for="nota1" class="form-label fw-bold">Nota 1</label>
          <input
            type="number"
            id="nota1"
            class="form-control"
            :class="{ 'is-invalid': nota1Invalida }"
            v-model.number="nota1"
            required
          />
          <div class="invalid-feedback" v-if="nota1 < 10">El valor debe ser superior o igual a 10</div>
          <div class="invalid-feedback" v-else-if="nota1 > 70">El valor debe ser inferior o igual a 70</div>
        </div>

        <!-- Nota 2 -->
        <div class="mb-3 text-center">
          <label for="nota2" class="form-label fw-bold">Nota 2</label>
          <input
            type="number"
            id="nota2"
            class="form-control"
            :class="{ 'is-invalid': nota2Invalida }"
            v-model.number="nota2"
            required
          />
          <div class="invalid-feedback" v-if="nota2 < 10">El valor debe ser superior o igual a 10</div>
          <div class="invalid-feedback" v-else-if="nota2 > 70">El valor debe ser inferior o igual a 70</div>
        </div>

        <!-- Nota 3 -->
        <div class="mb-3 text-center">
          <label for="nota3" class="form-label fw-bold">Nota 3</label>
          <input
            type="number"
            id="nota3"
            class="form-control"
            :class="{ 'is-invalid': nota3Invalida }"
            v-model.number="nota3"
            required
          />
          <div class="invalid-feedback" v-if="nota3 < 10">El valor debe ser superior o igual a 10</div>
          <div class="invalid-feedback" v-else-if="nota3 > 70">El valor debe ser inferior o igual a 70</div>
        </div>

        <!-- Asistencia -->
        <div class="mb-3 text-center">
          <label for="asistencia" class="form-label fw-bold">Asistencia %</label>
          <input
            type="number"
            id="asistencia"
            class="form-control"
            :class="{ 'is-invalid': asistenciaInvalida }"
            v-model.number="asistencia"
            required
          />
          <div class="invalid-feedback" v-if="asistencia < 0">El valor debe ser superior o igual a 0</div>
          <div class="invalid-feedback" v-else-if="asistencia > 100">El valor debe ser inferior o igual a 100</div>
        </div>

        <!-- Botón -->
        <div class="text-center">
          <button type="submit" class="btn btn-primary">Calcular</button>
        </div>

        <!-- Mensaje de error general -->
        <div v-if="error" class="text-danger mt-3 text-center">
          {{ error }}
        </div>

        <!-- Resultado -->
        <div v-if="promedioFinal !== null && estado !== null" class="mt-3 text-center">
          <p><strong>El promedio es:</strong> {{ promedioFinal }}</p>
          <p><strong>Tu estado es:</strong> {{ estado }}</p>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const nota1 = ref(null)
const nota2 = ref(null)
const nota3 = ref(null)
const asistencia = ref(null)

const promedioFinal = ref(null)
const estado = ref(null)
const error = ref('')

// Validadores
const nota1Invalida = computed(() => nota1.value !== null && (nota1.value < 10 || nota1.value > 70))
const nota2Invalida = computed(() => nota2.value !== null && (nota2.value < 10 || nota2.value > 70))
const nota3Invalida = computed(() => nota3.value !== null && (nota3.value < 10 || nota3.value > 70))
const asistenciaInvalida = computed(() => asistencia.value !== null && (asistencia.value < 0 || asistencia.value > 100))

function calcularPromedio() {
  error.value = ''
  promedioFinal.value = null
  estado.value = null

  const notas = [nota1.value, nota2.value, nota3.value]

  if (
    notas.some(n => n < 10 || n > 70) ||
    asistencia.value < 0 || asistencia.value > 100
  ) {
    error.value = 'Por favor, ingrese valores válidos para las notas y la asistencia'
    return
  }

  const promedio = (nota1.value * 0.35) + (nota2.value * 0.35) + (nota3.value * 0.3)
  promedioFinal.value = promedio.toFixed(2)
  estado.value = (promedio >= 40 && asistencia.value >= 80) ? 'Aprobado' : 'Reprobado'
}
</script>
