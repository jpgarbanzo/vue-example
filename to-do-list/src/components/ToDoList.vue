<template>
  <h1>{{ titulo }}</h1>
  <div class="formulario">
    <input v-model="tareaNueva" />
    <button v-on:click="agregarElemento">Add</button>
  </div>

  {{ tareaNueva }}

  <h2>Task List</h2>

  <ul>
    <li v-for="(tarea, index) in listaDeTareas" v-bind:key="index">
      {{ index }}-{{ tarea }}
      <button v-on:click="eliminarElemento(index)">Delete</button>
    </li>
  </ul>

  <h2>Tareas eliminadas</h2>
  <ul>
    <li v-for="(tarea, index) in tareasEliminadas" v-bind:key="index">{{ index }}-{{ tarea }}</li>
  </ul>

  <!-- <pre>
    {{ listaDeTareas }}
  </pre>
  <pre> {{ tareasEliminadas }}</pre> -->
</template>

<script>
export default {
  data() {
    return {
      titulo: 'Aprendizaje de Vue',
      listaDeTareas: ['Instalar Vue', 'Abrirlo en el navegador'],
      tareaNueva: 'La tarea que crea la persona',
      tareasEliminadas: [],
    }
  },

  methods: {
    agregarElemento() {
      this.listaDeTareas.push(this.tareaNueva)
    },

    eliminarElemento(index) {
      //   alert('Eliminar elemento en la posición #' + index)
      this.tareasEliminadas.push(this.listaDeTareas[index])

      this.listaDeTareas.splice(index, 1)
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
