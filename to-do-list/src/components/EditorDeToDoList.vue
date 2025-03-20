<template>
  <section>
    <h1>Editar to-do: {{ indice }}-{{ tarea }}</h1>
    <input v-bind:value="tarea" />
    <button>Guardar</button>

    <h1>{{ textoDeEjmplo }}</h1>
  </section>
</template>

<script>
export default {
  props: {
    tarea: {
      type: String,
    },
    indice: {
      type: Number,
    },
    fecha: {
      type: String,
    },
    textoDeEjmplo: {
      type: String,
    },
  },
}
</script>
