<template>
  <h1>{{ titulo }}</h1>
  <div class="formulario">
    <input v-model="tareaNueva" />
    <button v-on:click="agregarElemento">Add</button>
  </div>

  {{ tareaNueva }}

  <h2>Task List</h2>

  <ul>
    <li v-for="tarea in listaDeTareas">
      {{ tarea }}
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      titulo: 'Aprendizaje de Vue',
      listaDeTareas: ['Instalar Vue', 'Abrirlo en el navegador'],
      tareaNueva: 'La tarea que crea la persona',
    }
  },

  methods: {
    agregarElemento() {
      alert('hola')
    },
  },
}
</script>

<style scoped>
h3 {
  color: black !important;
}

.formulario {
  display: block;
  background-color: red;
}
</style>
