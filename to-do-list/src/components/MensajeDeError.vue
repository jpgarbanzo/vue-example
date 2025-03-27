<template>
  <p v-if="!valido">Por favor, agregue solamente números</p>
</template>

<script>
export default {
  data() {
    return {
      valido: true,
    }
  },

  methods: {
    validar(textoNumerico) {
      console.log('validando el valor ' + textoNumerico)
      this.valido = Number.isInteger(parseInt(textoNumerico))
    },
  },
}
</script>
