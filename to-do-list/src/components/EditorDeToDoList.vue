<template>
  <section>
    <h1>Editar to-do: {{ indice }}-{{ tarea }}</h1>
    <input v-bind:value="tarea" />
    <button v-on:click="notificarPadre">Guardar</button>

    <!-- <h1>{{ textoDeEjmplo }}</h1> -->
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
    // fecha: {
    //   type: String,
    // },
    // textoDeEjmplo: {
    //   type: String,
    // },
  },

  methods: {
    notificarPadre() {
      this.$emit('edit', {
        tarea: this.tarea,
        indice: this.indice,
      })
    },
  },
}
</script>
