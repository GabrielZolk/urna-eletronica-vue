<template>
  <div class="urna-tela">
    <div v-if="tela != 'fim'" class="tela-voto">
      <div class="tela-voto-textos">
        <div class="tela-voto-titulo">Seu voto para:</div>
        <div class="tela-voto-tipo">{{ tela }}</div>
        <div class="tela-voto-nums">
          Números

          <div
            class="tela-voto-num"
            v-for="(value, key) in numeroVoto.padEnd(quantidadeNums, ' ')"
            :key="key"
          >
            {{ value }}
          </div>
        </div>
        <div class="tela-voto-descricao">
          Nome: <strong>{{ candidato.nome ? candidato.nome : "__________" }}</strong>
        </div>

        <div class="tela-voto-descricao">
          Partido:
          <strong>{{ candidato.partido ? candidato.partido : "__________" }}</strong>
        </div>
      </div>

      <div v-if="candidato.imagem" class="tela-voto-img">
        <img :src="candidato.imagem"/>
      </div>

      <div class="tela-voto-instrucoes">
        <p>Aperte a tecla:</p>
        <p>BRANCO para VOTAR EM BRANCO</p>
        <p>LARANJA para CORRIGIR</p>
        <p>VERDE para CONFIRMAR</p>
      </div>
    </div>
    <div v-if="tela == 'fim'" class="tela-fim">FIM</div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Tela",
  props: {
    tela: String,
    numeroVoto: String,
    quantidadeNums: Number,
    candidato: Object,
  },
};
</script>

<style>
.urna-tela {
  width: 55%;
  height: 100%;
  background-color: var(--ballot-box-screen-color);
  border-radius: 5px;
  border: 2px solid var(--light-border-color);
  padding: 20px;
  color: var(--dark-text-color);
}

.tela-voto {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    height: 100%;
}

.tela-voto-textos {
    flex: 1;
}

.tela-voto-titulo {
  font-size: 20px;
}

.tela-voto-tipo {
  font-size: 30px;
  font-weight: bold;
  margin: 20px 0;
  text-transform: uppercase;
}

.tela-voto-nums {
  display: flex;
  align-items: center;
}

.tela-voto-num {
  width: 45px;
  height: 55px;
  border: 1px solid var(--dark-border-color);
  margin-left: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 30px;
}

.tela-voto-descricao {
    margin-top: 20px;
}

.tela-voto-img img {
    width: 110px;
    height: 150px;
    border: 1px solid var(--dark-border-color);
}

.tela-voto-instrucoes {
    width: 100%;
    border-top: 1px solid var(--dark-border-color);
    font-size: 13px;
    margin-top: 20px;
    padding-top: 10px;
}

.tela-fim {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 120px;
    width: 100%;
    height: 100%;
}
</style>