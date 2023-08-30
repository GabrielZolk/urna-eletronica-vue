<template>
  <div class="urna-teclado">
    <div class="teclado-numerico">
      <div class="teclado-numerico-linha">
        <button v-on:click="addNum(1)">1</button>
        <button v-on:click="addNum(2)">2</button>
        <button v-on:click="addNum(3)">3</button>
      </div>
      <div class="teclado-numerico-linha">
        <button v-on:click="addNum(4)">4</button>
        <button v-on:click="addNum(5)">5</button>
        <button v-on:click="addNum(6)">6</button>
      </div>
      <div class="teclado-numerico-linha">
        <button v-on:click="addNum(7)">7</button>
        <button v-on:click="addNum(8)">8</button>
        <button v-on:click="addNum(9)">9</button>
      </div>
      <div class="teclado-numerico-linha">
        <button v-on:click="addNum(0)">0</button>
      </div>
    </div>
    <div class="teclado-acoes">
        <button class="btn-branco" v-on:click="votarEmBranco()">BRANCO</button>
        <button class="btn-corrige" v-on:click="corrigir()">CORRIGE</button>
        <button class="btn-confirma" v-on:click="confirmar()">CONFIRMA</button>
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Teclado",
  props: {
    addNum: Function,
    corrigir: Function,
    confirmar: Function,
    votarEmBranco: Function,
  }
};
</script>

<style>
    .urna-teclado {
        width: 40%;
        height: 100%;
        background-color: var(--ballot-box-keyboard-color);
        border-radius: 5px;
        padding: 20px;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
    }

    .teclado-numerico {
        width: 100%;
    }

    .teclado-numerico-linha {
        display: flex;
        justify-content: space-around;
        margin-bottom: 20px;
    }

    .teclado-numerico button {
        background-color: var(--ballot-box-keyboard-button-color);
        color: var(--light-text-color);
        font-size: 30px;
        border-radius: 5px;
        width: 80px;
        height: 50px;
    }

    .teclado-acoes {
        width: 100%;
        display: flex;
        justify-content: space-around;
    }

    .teclado-acoes button {
        color: var(--dar-text-color);
        font-size: 15px;
        border-radius: 5px;
        width: 30%;
        height: 50px;
    }

    .btn-branco {
        background-color: var(--ballot-box-white-button-color);
    }

    .btn-corrige {
        background-color: var(--ballot-box-correct-button-color);
    }

    .btn-confirma {
        background-color: var(--ballot-box-confirm-button-color);
    }

</style>
