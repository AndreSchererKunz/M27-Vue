<script setup>
import { reactive } from 'vue';

const nome = "gian souza"
const meuObj = {
  nome: "gian",
  filmeFavorito: "Rocky"
}

function dizOla(nome) {
  return `${nome} diz oi`;
}

const enderecoDaImagemBatman = "https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2F3.bp.blogspot.com%2F-_bEuWkDoh4M%2FWlnaJ5rrFsI%2FAAAAAAAAAJU%2Fs2cWMTglbp0OEpI7cdpvDQsAf3IzOG1agCLcBGAs%2Fs1600%2Fbatman.jpg&f=1&nofb=1&ipt=1407e09258b51eacc1704e5309d042db2bae30992c2866cfa549282b55638671&ipo=images"
const imagemSuper = "https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fimages.hdqwalls.com%2Fdownload%2Fsuperman-2020-07-1920x1080.jpg&f=1&nofb=1&ipt=773de3c811e669b11fd02fbecfc6c373610dafaedc20350f26401b6791d567ef&ipo=images"

const botaoEstaDesabilitado = false;

const gostaDoBatman = false;
const gostaDoSuperman = false;

const estaAutorizado = false;

// let contador = 0;
const estado = reactive({
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
  nomes: ['gian', 'paulo', 'luisa', 'monica'],
  nomeAInserir: '',
})

function incrementar() {
  estado.contador++;
}

function decrementar() {
  estado.contador--;
}

function alteraEmail(evento) {
  estado.email = evento.target.value;
}

function mostraSaldoFuturo() {
  const { saldo, transferindo} = estado;
  return saldo - transferindo;
  // return estado.saldo - estado.transferindo;
}

function validaValorDeTransferencia() {
  const { saldo, transferindo} = estado;
  return saldo >= transferindo;
}

function cadastrarNome() {
  if (estado.nome.length >= 3) {
    estado.nomes.push(estado.nomeAInserir)
  } else {
    alert("Digite mais caracteres")
  }
}

</script>

<template>
  <h1>{{ dizOla("paula") }}</h1>
  <img v-if="gostaDoBatman" :src="enderecoDaImagemBatman" alt="">
  <img v-else-if="gostaDoSuperman" :src="imagemSuper" alt="">
  <h2 v-else>Não curte heróis da DC</h2>

  <h1 v-if="estaAutorizado">Bem-vindo</h1>
  <h1 v-else>Não possui acesso</h1>

  <button :disabled="botaoEstaDesabilitado">enviar mensagem</button>

  <br />
  <hr />

  {{ estado.contador }}

  <button @click="incrementar" type="button">+</button>
  <button @click="decrementar" type="button">-</button>

  <br />
  <hr />

  {{ estado.email }}
  <input type="email" @keyup="alteraEmail">

  <br />
  <hr />

  Saldo: {{ estado.saldo }} <br />
  Transferindo: {{ estado.transferindo }} <br />
  Saldo depois da transferência? {{ mostraSaldoFuturo() }} <br />
  <input class="campo" :class="{ invalido: !validaValorDeTransferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir">
  <button v-if="validaValorDeTransferencia()">Transferir</button>
  <span v-else>Valor maior que o saldo</span>

  <br />
  <hr />

  <ul>
    <li v-for="nome in estado.nomes">
      {{ nome }}
    </li>
  </ul>
  <input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
  <button @click="cadastrarNome" type="button">Cadastrar nome</button>

  <h3 v-for="nome in estado.nomes">{{ nome }}</h3>
</template>

<style scoped>
img {
  max-width: 200px;
}

.invalido {
  outline-color: red;
  border-color: red;
}

.cMPO {
  border: 2px solid black;
}
</style>
