<template>
  <div>
    <h1>Calculadora de IMC</h1>
    <form @submit.prevent="calcular">
      <div>
        <label for="peso">Peso (kg):</label>
        <input type="number" id="peso" v-model="peso" step="0.01" required>
      </div>
      <div>
        <label for="altura">Altura (m):</label>
        <input type="number" id="altura" v-model="altura" step="0.01" required>
      </div>
      <div>
        <button type="submit">Calcular</button>
      </div>
      <div>
        <label v-if="mensagem">{{ mensagem }}</label>
        <br>
        <label v-if="aviso">{{ aviso }}</label>
        <br>
        <img :src= imagem :class="{ 'imagem-redimensionada': imagem }"  v-if="imagem">
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
  name: "CalculadoraImc",

  data() {
    return {
      peso: null as number | null,
      altura: null as number | null,
      imc: null as number | null,
      mensagem: "" as string,
      aviso: "" as string,
      imagem:"" ,
    };
  },
  methods: {
    calcular() {
      if (this.peso !== null && this.altura !== null) {
        const peso = parseFloat(this.peso.toString());
        const altura = parseFloat(this.altura.toString());
        const imc = peso / (altura * altura);
        this.imc = parseFloat(imc.toFixed(2));
        this.aviso = `É importante levar em consideração que o peso 
          não necessariamente significa que a pessoa é obesa. 
          Ou seja, depende da composição corporal.`
        if (imc < 18.5 ) {
          this.mensagem = `Possui um IMC de ${this.imc}: Abaixo do Peso.`;
          this.imagem = require('@/assets/abaixo do peso.jpg');
        } else if (imc >= 18.6 && imc <= 24.9) {
          this.mensagem = `Possui um IMC de ${this.imc}:peso normal.`;
          this.imagem = require('@/assets/peso normal.jpg');
        }
          else if (imc >= 25 && imc <= 29.9) {
          this.mensagem = `Possui um IMC de ${this.imc}: Levemente acima do Peso.`;
          this.imagem = require('@/assets/levemente acima do peso.jpg');
        } else if (imc >= 30 && imc <= 34.9) {
          this.mensagem = `Possui um IMC de ${this.imc}: Obesidade grau I.`;
          this.imagem = require('@/assets/obesidade grau 1.jpg');
        } else if (imc >= 35 && imc <= 39.9) {
          this.mensagem = `Possui um IMC de ${this.imc}: Obesidade grau II.`;
          this.imagem = require('@/assets/obesidade grau 2.jpg');
        } else if (imc >= 40) {
          this.mensagem = `Possui um IMC de ${this.imc}: Obesidade grau III.`;
          this.imagem = require('@/assets/obesidade grau 3.jpg');
        }
      }
    },
  }
});
</script>
<style>
.imagem-redimensionada {
  max-width: 400px;
  max-height: 400px;
}</style>