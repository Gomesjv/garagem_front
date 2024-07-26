<script setup>
import { ref, reactive, onMounted } from "vue";
import CoresApi from "@/api/cores";
const coresApi = new CoresApi();

const defaultCor = { id: null, descricao: "" };
const cores = ref([]);
const cor = reactive({ ...defaultCor });

onMounted(async () => {
  cores.value = await coresApi.buscarTodasAsCores();
});

function limpar() {
  Object.assign(cor, { ...defaultCor });
}

async function salvar() {
  if (cor.id) {
    await coresApi.atualizarCor(cor);
  } else {
    await coresApi.adicionarCor(cor);
  }
  cores.value = await coresApi.buscarTodasAsCores();
  limpar();
}

function editar(cor_para_editar) {
  Object.assign(cor, cor_para_editar);
}

async function excluir(id) {
  await coresApi.excluirCor(id);
  cores.value = await coresApi.buscarTodasAsCores();
  limpar();
}
</script>

<template>
  <h1>Cor</h1>
  <hr />
  <div class="form">
    <input type="text" v-model="cor.descricao" placeholder="Descrição" class="input"/>
    <button @click="salvar" class="btn-enviar">Salvar</button>
  </div>
  <hr />
  <ul>
    <li v-for="cor in cores" :key="cor.id">
      <span @click="editar(cor)">
        ({{ cor.id }}) - {{ cor.descricao }} -
      </span>
      <button @click="excluir(cor.id)">X</button>
    </li>
  </ul>
</template>

<style scoped>
  .form {
        display: flex;
        flex-direction: column;
        width: 50%;
        margin: auto;
        min-width: 250px;
        gap: 20px;
        padding: 10px;
    }

    .input {
        border: none;
        background-color: #ddd;
        border-radius: 10px;
        padding: 5px 10px;
    }

    .btn-enviar {
        background-color: transparent;
        border-radius: 20px;
        padding: 10px 20px;
        font-weight: bolder;
        text-transform: uppercase;
    }
</style>
