<script setup>
import VeiculosApi from '@/api/veiculos';
import ModelosApi from '@/api/modelos';
import CoresApi from '@/api/cores';
import { ref } from 'vue';
import { onMounted } from 'vue';
import AcessoriosApi from '@/api/acessorios';
import { useUploaderStore } from '@/stores/uploader';
import { reactive } from 'vue';
import VeiculoCard from '@/components/VeiculoCard.vue';

const uploaderStore = useUploaderStore()
const veiculosApi = new VeiculosApi();
const modelosApi = new ModelosApi();
const coresApi = new CoresApi();
const acessoriosApi = new AcessoriosApi()

const file = ref(null);
const previewImage = ref('');

const veiculos = ref();
const veiculo = reactive({
    ano: "",
    preco: "",
    modelo: "",
    cor: "",
    acessorios: "",
    foto_veiculo_attachment_key: '',
})
const modelos = ref();
const modelo = ref();
const cores = ref()
const cor = ref()
const acessorios = ref()
const acessoriosEscolhidos = ref()

async function salvar() {
    veiculo.foto_veiculo_attachment_key = await uploaderStore.uploadImage(file.value);
    await veiculosApi.adicionarVeiculo(veiculo)
    veiculos.value = await veiculosApi.buscarTodosOsVeiculos()
}

const uploadImage = (e) => {
  file.value = e.target.files[0];
  previewImage.value = URL.createObjectURL(e.target.files[0]);
};

async function deletar(id) {
    await veiculosApi.excluirVeiculo(id)
    veiculos.value = await veiculosApi.buscarTodosOsVeiculos()
}

onMounted(async () => {
    veiculos.value = await veiculosApi.buscarTodosOsVeiculos()
    modelos.value = await modelosApi.buscarTodosOsModelos()
    cores.value = await coresApi.buscarTodasAsCores()
    acessorios.value = await acessoriosApi.buscarTodosOsAcessorios()
})
</script>

<template>
    <main>
        <div class="form">
            <input type="number" placeholder="Ano" v-model="veiculo.ano" class="input"/>
            <input type="number" placeholder="Preco" v-model="veiculo.preco" class="input">
            <select v-model="veiculo.modelo" class="input">
                <option value="" selected disabled>Modelo</option>
                <option v-for="modelo in modelos" :value="modelo.id">{{ modelo.nome }}</option>
            </select>
            <select v-model="veiculo.cor" class="input" placeholder="Cor">
                <option value="" selected disabled>Cor</option>
                <option v-for="cor in cores" :value="cor.id">{{ cor.descricao }}</option>
            </select>
            <select v-model="veiculo.acessorios" multiple class="input">
                <option value="" selected disabled>Acessorios</option>
                <option v-for="acessorio in acessorios" :value="acessorio.id">{{ acessorio.descricao }}</option>
            </select>
            <input type="file" id="image" @change="uploadImage" />
            <img v-if="previewImage" :src="previewImage" class="previewImage" alt="preview" />

            <button @click="salvar" class="btn-enviar">
                Enviar
            </button>
        </div>

        <div class="veiculos">
            <VeiculoCard v-for="veiculo in veiculos" :item="veiculo" @deletar="deletar" :deletar="true" ></VeiculoCard>
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

    .veiculos {
        display: flex;
        flex-wrap: wrap;
        padding: 10px 20px;
        align-items: center;
        justify-content: space-around;
    }
</style>