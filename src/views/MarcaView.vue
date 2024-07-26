<script setup>
import { ref, reactive, onMounted } from "vue";
import MarcasApi from "@/api/marcas";
const marcasApi = new MarcasApi();

const defaultMarca = { id: null, descricao: "" };
const marcas = ref([]);
const marca = reactive({ ...defaultMarca });

onMounted(async () => {
  marcas.value = await marcasApi.buscarTodasAsMarcas();
});

function limpar() {
  Object.assign(marca, { ...defaultMarca });
}

async function salvar() {
  if (marca.id) {
    await marcasApi.atualizarMarca(marca);
  } else {
    await marcasApi.adicionarMarca(marca);
  }
  marcas.value = await marcasApi.buscarTodasAsMarcas();
  limpar();
}

function editar(marca_para_editar) {
  Object.assign(marca, marca_para_editar);
}

async function excluir(id) {
  await marcasApi.excluirMarca(id);
  marcas.value = await marcasApi.buscarTodasAsMarcas();
  limpar();
}
</script>

<template>
  <h1>Marca</h1>
  <hr />
  <div class="form">
    <input type="text" v-model="marca.descricao" placeholder="Descrição" class="input"/>
    <button @click="salvar" class="btn-enviar" >Salvar</button>
  </div>
  <hr />
  <ul>
    <li v-for="marca in marcas" :key="marca.id">
      <span @click="editar(marca)">
        ({{ marca.id }}) - {{ marca.descricao }} -
      </span>
      <button @click="excluir(marca.id)">X</button>
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
