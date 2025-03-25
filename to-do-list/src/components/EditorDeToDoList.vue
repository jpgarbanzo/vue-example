<template>
  <section>
    <h1>Editar to-do: {{ indice }}-{{ tarea }}</h1>
    <input v-model="valorActualizado" />
    <button v-on:click="notificarPadre">Guardar</button>
    <h2>Valor nuevo es: {{ valorActualizado }}</h2>
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

  mounted() {
    this.valorActualizado = this.tarea
  },

  data() {
    return {
      valorActualizado: '',
    }
  },

  methods: {
    notificarPadre() {
      this.$emit('edit', {
        tarea: this.valorActualizado,
        indice: this.indice,
      })
    },

    actualiceValor(valorDelInput) {
      this.valorActualizado += valorDelInput.data
    },
  },
}
</script>
