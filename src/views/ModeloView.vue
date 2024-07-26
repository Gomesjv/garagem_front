<script setup>
import CategoriasApi from '@/api/categorias';
import MarcasApi from '@/api/marcas';
import ModelosApi from '@/api/modelos';
import { ref } from 'vue';
import { onMounted } from 'vue';
import { reactive } from 'vue';

const modelosApi = new ModelosApi();
const marcasApi = new MarcasApi();
const categoriasApi = new CategoriasApi()

const modelo = reactive({
    nome: "",
    marca: "",
    categoria: ""
});
const modelos = ref();
const marcas = ref()
const categorias = ref()


async function salvar() {
    await modelosApi.adicionarModelo(modelo)
}

onMounted(async () => {
    modelos.value = await modelosApi.buscarTodosOsModelos()
    marcas.value = await marcasApi.buscarTodasAsMarcas()
    categorias.value = await categoriasApi.buscarTodasAsCategorias()
})
</script>

<template>
    <main>
        <div class="form">
            <input type="text" placeholder="Nome" v-model="modelo.nome" class="input"/>
            <select v-model="modelo.marca" class="input" placeholder="Cor">
                <option value="" selected disabled>Marca</option>
                <option v-for="marca in marcas" :value="marca.id">{{ marca.descricao }}</option>
            </select>
            <select v-model="modelo.categoria" class="input">
                <option value="" selected disabled>Categorias</option>
                <option v-for="categoria in categorias" :value="categoria.id">{{ categoria.descricao }}</option>
            </select>

            <button @click="salvar" class="btn-enviar">
                Enviar
            </button>
        </div>
    </main>
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