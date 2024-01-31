<script setup>
import { reactive } from 'vue';

const estado = reactive({
  opcao: '',
  num1: 0,
  num2: 0
})

const divideNumeros = () => {
  const numTemp = estado.num2;

  if(numTemp == 0){
    return "Não é possível realizar uma divisão pelo número 0!"
  }else{
    return estado.num1 / estado.num2
  }
}

const calculaValor = () => {
  const {opcao} = estado;

  switch (opcao){
    case 'soma':
      return Number(estado.num1) + Number(estado.num2);
    case 'subtracao':
      return estado.num1 - estado.num2;
    case 'multiplicacao':
      return estado.num1 * estado.num2;
    case 'divisao':
      return divideNumeros();
  }

  estado.num1 = 0;
  estado.num2 = 0;
  estado.opcao = '';
}



</script>

<template>
  <div class="container">
    <header class="cabecalho">
      <h1 class="titulo">Calculadora Aritmética</h1>
    </header>
    <form class="formulario">
      <input type="number" placeholder="Insira o primeiro número" @keyup="evento => estado.num1 = evento.target.value">
      <input  type="number" required placeholder="Insira o segundo número" @keyup="evento => estado.num2 = evento.target.value">
      <select v-model="estado.opcao" required @keyup="evento => estado.opcao = evento.target.value">
        <option disabled value="">Selecione operação</option>
        <option value="soma">Somar</option>
        <option value="subtracao">Subtrair</option>
        <option value="multiplicacao">Multiplicar</option>
        <option value="divisao">Dividir</option>
      </select>
    </form>
    <p>Resultado: {{ (calculaValor()) }}</p>
  </div>
</template>

<style scoped>
  .container{
    max-width: 960px;
    width: 100%;
    margin: 0 auto;
    
    .cabecalho{
        background-color: rgb(44, 6, 87);
    }

    .titulo{
        padding: 24px;
        text-align: center;
        color: rgb(237, 237, 247);
    }

    .formulario{
      display: flex;
      justify-content: space-between;
      padding-bottom: 24px;
    }

    .formulario input{
      font-size: 24px;
      border: none;
      border-bottom: 2px solid rgb(44, 6, 87);
      padding: 8px;
      text-align: center;
    }

    .formulario select{
      font-size: 24px;
      padding: 16px;
      border-color: rgb(44, 6, 87);
    }

    p{
      border: 2px solid rgb(44, 6, 87);
      padding: 24px;
      font-size: 24px;
      text-align: center;
    }
  }
</style>
