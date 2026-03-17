<script setup>
import { ref } from 'vue'

const encargado = ref('')
const carnet1 = ref('')
const carnet2 = ref('')
const carnet3 = ref('')
const cubiculo = ref('')
const tiempo = ref('')
const alquileres = ref([])
const error = ref('')
const mostrarLista = ref(true)

const patronCarnet = /^SMSS\d{6}$/

function validarCarnet(carnet) {
  return patronCarnet.test(carnet.trim().toUpperCase())
}

function registrarAlquiler() {
  if (
    encargado.value.trim() === '' ||
    carnet1.value.trim() === '' ||
    carnet2.value.trim() === '' ||
    carnet3.value.trim() === '' ||
    cubiculo.value === '' ||
    tiempo.value === ''
  ) {
    error.value = 'Todos los campos son obligatorios.'
    return
  }

  if (
    !validarCarnet(carnet1.value) ||
    !validarCarnet(carnet2.value) ||
    !validarCarnet(carnet3.value)
  ) {
    error.value = 'Los carnets deben tener formato como SMSS042024.'
    return
  }

  const c1 = carnet1.value.trim().toUpperCase()
  const c2 = carnet2.value.trim().toUpperCase()
  const c3 = carnet3.value.trim().toUpperCase()

  if (c1 === c2 || c1 === c3 || c2 === c3) {
    error.value = 'Los tres carnets deben ser diferentes.'
    return
  }

  alquileres.value.push({
    id: Date.now(),
    encargado: encargado.value.trim(),
    carnet1: c1,
    carnet2: c2,
    carnet3: c3,
    cubiculo: cubiculo.value,
    tiempo: tiempo.value
  })

  encargado.value = ''
  carnet1.value = ''
  carnet2.value = ''
  carnet3.value = ''
  cubiculo.value = ''
  tiempo.value = ''
  error.value = ''
}

function eliminarAlquiler(id) {
  alquileres.value = alquileres.value.filter(alquiler => alquiler.id !== id)
}

function cambiarVista() {
  mostrarLista.value = !mostrarLista.value
}
</script>

<template>
  <div class="contenedor">
    <h1>Sistema de Alquiler de Cubículos</h1>
    <p class="descripcion">
      Registra el préstamo de cubículos de biblioteca usando tres carnets estudiantiles y un tiempo de uso.
    </p>

    <form class="formulario" @submit.prevent="registrarAlquiler">
      <label for="encargado">Nombre del estudiante encargado</label>
      <input
        id="encargado"
        type="text"
        v-model="encargado"
        placeholder="Ejemplo: Brenda López"
      />

      <label for="carnet1">Carnet 1</label>
      <input
        id="carnet1"
        type="text"
        v-model="carnet1"
        placeholder="Ejemplo: SMSS042024"
      />

      <label for="carnet2">Carnet 2</label>
      <input
        id="carnet2"
        type="text"
        v-model="carnet2"
        placeholder="Ejemplo: SMSS052024"
      />

      <label for="carnet3">Carnet 3</label>
      <input
        id="carnet3"
        type="text"
        v-model="carnet3"
        placeholder="Ejemplo: SMSS062024"
      />

      <label for="cubiculo">Cubículo</label>
      <select id="cubiculo" v-model="cubiculo">
        <option disabled value="">Seleccione un cubículo</option>
        <option>Cubículo 1</option>
        <option>Cubículo 2</option>
        <option>Cubículo 3</option>
        <option>Cubículo 4</option>
        <option>Cubículo 5</option>
      </select>

      <label for="tiempo">Tiempo de alquiler</label>
      <select id="tiempo" v-model="tiempo">
        <option disabled value="">Seleccione el tiempo</option>
        <option>30 minutos</option>
        <option>1 hora</option>
        <option>2 horas</option>
        <option>3 horas</option>
      </select>

      <div class="botones">
        <button type="submit">Registrar alquiler</button>
        <button type="button" @click="cambiarVista">
          {{ mostrarLista ? 'Ocultar registros' : 'Mostrar registros' }}
        </button>
      </div>
    </form>

    <p v-if="error" class="error">{{ error }}</p>

    <section v-if="mostrarLista" class="lista">
      <h2>Total de alquileres: {{ alquileres.length }}</h2>

      <ul v-if="alquileres.length > 0">
        <li
          v-for="alquiler in alquileres"
          :key="alquiler.id"
          :title="'Reserva de ' + alquiler.encargado"
          class="tarjeta"
        >
          <h3>{{ alquiler.encargado }}</h3>
          <p><strong>Cubículo:</strong> {{ alquiler.cubiculo }}</p>
          <p><strong>Tiempo:</strong> {{ alquiler.tiempo }}</p>
          <p><strong>Carnet 1:</strong> {{ alquiler.carnet1 }}</p>
          <p><strong>Carnet 2:</strong> {{ alquiler.carnet2 }}</p>
          <p><strong>Carnet 3:</strong> {{ alquiler.carnet3 }}</p>
          <button class="eliminar" @click="eliminarAlquiler(alquiler.id)">
            Eliminar
          </button>
        </li>
      </ul>

      <p v-else>No hay alquileres registrados todavía.</p>
    </section>
  </div>
</template>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f2f5fb;
}

.contenedor {
  max-width: 900px;
  margin: 30px auto;
  background: white;
  padding: 25px;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.12);
}

h1,
h2,
h3 {
  color: #1d3c78;
}

.descripcion {
  margin-bottom: 20px;
  color: #444;
}

.formulario {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

label {
  font-weight: bold;
  margin-top: 5px;
}

input,
select,
button {
  padding: 10px;
  font-size: 15px;
  border-radius: 8px;
}

input,
select {
  border: 1px solid #cfcfcf;
}

.botones {
  display: flex;
  gap: 10px;
  margin-top: 10px;
}

button {
  border: none;
  background: #1d3c78;
  color: white;
  cursor: pointer;
}

button:hover {
  background: #152f5d;
}

.error {
  margin-top: 15px;
  color: #c62828;
  font-weight: bold;
}

.lista {
  margin-top: 25px;
}

.tarjeta {
  list-style: none;
  background: #eef4ff;
  padding: 15px;
  border-radius: 10px;
  margin-bottom: 12px;
  border-left: 5px solid #1d3c78;
}

.eliminar {
  margin-top: 10px;
  background: #c62828;
}

.eliminar:hover {
  background: #991b1b;
}
</style>