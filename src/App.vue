<template>
  <div id="app">
    <Calculadora_Imc />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Calculadora_Imc from './components/Calculadora_Imc.vue';
export default defineComponent({
  name: 'App',
  components: {
    Calculadora_Imc,
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

}
</style>