<template>
  <h1>{{ titulo }}</h1>
  <div class="formulario">
    <input v-model="tareaNueva" v-on:keydown.enter="agregarElemento" />
    <button v-on:click="agregarElemento" v-bind:disabled="deshabilitar">Add</button>
  </div>
  <mensaje-de-error ref="mensaje" />

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
    v-bind:tareaNueva="tareaNueva"
  />

  <!-- <pre>
    {{ listaDeTareas }}
  </pre>
  <pre> {{ tareasCompletadas }}</pre> -->
</template>

<script>
import EditorDeToDoList from './EditorDeToDoList.vue'
import MensajeDeError from './MensajeDeError.vue'

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

      deshabilitar: false,
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
      this.tareaNueva = ''
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

  watch: {
    tareaNueva: {
      immediate: true,
      handler() {
        if (this.$refs.mensaje) {
          this.$refs.mensaje.validar(this.tareaNueva)
        }

        if (this.tareaNueva.length === 0) {
          this.deshabilitar = true
        } else if (this.tareaNueva.length > 100) {
          this.deshabilitar = true
        } else {
          this.deshabilitar = false
        }
      },
    },
  },

  components: {
    'editor-de-to-do-list': EditorDeToDoList,
    'mensaje-de-error': MensajeDeError,
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
