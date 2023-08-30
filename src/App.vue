<template>
  <div id="app">
    <div class="urna">
      <Tela
        :tela="tela"
        :numeroVoto="numeroVoto"
        :quantidadeNums="quantidadeNums"
        :candidato="candidato"
      />
      <Teclado
        :addNum="addNum"
        :corrigir="corrigir"
        :confirmar="confirmar"
        :votarEmBranco="votarEmBranco"
      />
    </div>
  </div>
</template>

<script>
import "@/css/global.css";
import Teclado from "@/components/Teclado";
import Tela from "@/components/Tela";
import confirmAudio from "./assets/audios/confirm.wav";
import keyAudio from "./assets/audios/key.wav";

export default {
  name: "App",
  components: {
    Teclado,
    Tela,
  },
  methods: {
    addNum(num) {
      this.execSom(keyAudio);

      if (this.numeroVoto.length == this.quantidadeNums) {
        return false;
      }

      this.numeroVoto += "" + num;

      this.verificarCandidato();
    },
    verificarCandidato() {
      if (this.numeroVoto.length < this.quantidadeNums) {
        return false;
      }

      if (this.candidatos[this.tela][this.numeroVoto]) {
        this.candidato = this.candidatos[this.tela][this.numeroVoto];
        return true;
      }

      this.candidato = {
        nome: "Voto nulo",
        partido: "Voto nulo",
        imagem: "",
      };
    },
    corrigir() {
      this.execSom(keyAudio);
      this.limpar();
    },
    limpar() {
      this.candidato = {};
      this.numeroVoto = "";
    },
    confirmar() {
      if (this.numeroVoto.length < this.quantidadeNums) {
        return false;
      }

      return this.avancarTela();
    },
    avancarTela() {
      if (this.tela == "vereador") {
        this.execSom(confirmAudio);
      }

      if (this.tela == "prefeito") {
        this.tela = "vereador";
        this.quantidadeNums = 5;
        return this.limpar();
      }

      this.tela = "fim";

      var instancia = this;

      setTimeout(function () {
        instancia.tela = "prefeito";
        instancia.quantidadeNums = 2;
        return instancia.limpar();
      }, 4000);
    },
    votarEmBranco() {
      if (this.tela == "fim") {
        return false;
      }

      this.limpar();
      this.avancarTela();
    },
    execSom(arquivo) {
      if (arquivo) {
        let audio = new Audio(arquivo);
        audio.play();
      }
    },
  },
  data() {
    return {
      tela: "prefeito",
      numeroVoto: "",
      quantidadeNums: 2,
      candidato: {},
      candidatos: {
        prefeito: {
          "01": {
            nome: "Ash",
            partido: "Pokemon",
            imagem:
              "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/ash.png",
          },
          "08": {
            nome: "Vegeta",
            partido: "Dragon Ball",
            imagem:
              "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/vegeta.png",
          },
        },
        vereador: {
          "01234": {
            nome: "Pikachu",
            partido: "Pokemon",
            imagem:
              "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/pikachu.png",
          },
          "08001": {
            nome: "Goku",
            partido: "Dragon Ball",
            imagem:
              "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/goku.png",
          },
        },
      },
    };
  },
};
</script>

<style>
#app {
  background-color: var(--background-color);
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.urna {
  width: 1000px;
  height: 500px;
  background-color: var(--ballot-box-background-color);
  padding: 30px;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
}
</style>
