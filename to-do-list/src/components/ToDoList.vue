<template>
  <h1>{{ titulo }}</h1>
  <div class="formulario">
    <input />
    <button>Add</button>
  </div>

  <h2>Task List</h2>

  <ul>
    <li>{{ listaDeTareas }}</li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      titulo: 'Aprendizaje de Vue',
      listaDeTareas: ['Instalar Vue'],
    }
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
