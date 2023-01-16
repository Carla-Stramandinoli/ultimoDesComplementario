<script setup>
import { ref } from 'vue';
import FormularioComponent from './components/FormularioComponent.vue';
import TablaFormulario from './components/TablaFormulario.vue';

const state = ref({
  datos: []
});


function imprimirTabla(event) {
  console.log(this.state.datos);
  this.state.datos.push(event);
}

</script>

<template>
  <FormularioComponent @enviar="imprimirTabla($event)" />
  <TablaFormulario :info=state.datos />
</template>