<template>
  <h1>{{ titulo }}</h1>
  <div class="formulario">
    <input v-model="tareaNueva" />
    <button v-on:click="agregarElemento">Add</button>
  </div>

  <h2>Tareas Pendientes</h2>
  <p v-if="tareasPendientes === 0">
    <span>No hay tareas pendientes</span>
  </p>
  <ul v-else>
    <li v-for="(tarea, index) in listaDeTareas" v-bind:key="index">
      {{ index }}-{{ tarea }}
      <button v-on:click="editarElemento(index, tarea)">Editar</button>
      <button v-on:click="eliminarElemento(index)">Completar</button>
    </li>
  </ul>

  <h2>Tareas Completadas</h2>
  <p v-if="contadorDeTareasCompletadas === 0">
    <span>No hay tareas completadas</span>
  </p>
  <ul v-else style="min-height: 100px; background-color: green">
    <li v-for="(tarea, index) in tareasCompletadas" v-bind:key="index">{{ index }}-{{ tarea }}</li>
  </ul>

  <h2>Resumen de tareas</h2>
  <p>Completadas: {{ contadorDeTareasCompletadas }} | Pendientes: {{ tareasPendientes }}</p>
  <p>Total de tareas: {{ totalDeTareas }}</p>

  <hr />
  Quiero editar la tarea: {{ tareaQueEstoyEditando }}
  <editor-de-to-do-list
    v-if="mostrarEditor"
    v-bind:tarea="tareaQueEstoyEditando"
    v-bind:indice="indiceQueEstoyEditando"
    v-on:edit="actualizarToDoList"
  />

  <!-- <pre>
    {{ listaDeTareas }}
  </pre>
  <pre> {{ tareasCompletadas }}</pre> -->
</template>

<script>
import EditorDeToDoList from './EditorDeToDoList.vue'

export default {
  data() {
    return {
      titulo: 'Aprendizaje de Vue',
      listaDeTareas: ['Instalar Vue', 'Abrirlo en el navegador'],
      tareaNueva: '',
      tareasCompletadas: [],

      mostrarEditor: false,
      tareaQueEstoyEditando: '',
      indiceQueEstoyEditando: null,

      fechaDeHoy: '19 de marzo de 2025',
    }
  },

  computed: {
    tareasPendientes() {
      return this.listaDeTareas.length
    },

    contadorDeTareasCompletadas() {
      return this.tareasCompletadas.length
    },

    totalDeTareas() {
      return this.tareasPendientes + this.contadorDeTareasCompletadas
    },
  },

  methods: {
    agregarElemento() {
      this.listaDeTareas.push(this.tareaNueva)
    },

    eliminarElemento(index) {
      //   alert('Eliminar elemento en la posición #' + index)
      this.tareasCompletadas.push(this.listaDeTareas[index])

      this.listaDeTareas.splice(index, 1)
    },

    editarElemento(index, tarea) {
      this.mostrarEditor = true
      this.tareaQueEstoyEditando = tarea
      this.indiceQueEstoyEditando = index
    },

    actualizarToDoList({ tarea, indice }) {
      alert('actualizar todo list desde el padre, tarea:' + tarea + ' ' + indice)

      this.listaDeTareas[indice] = tarea
    },
  },

  components: {
    'editor-de-to-do-list': EditorDeToDoList,
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
