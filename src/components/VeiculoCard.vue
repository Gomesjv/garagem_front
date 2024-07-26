<script setup>
defineProps(["item", "deletar"])
</script>

<template>
    <div class="card">
        <img v-if="item.foto_veiculo" :src="item.foto_veiculo.url" alt="" width="300px">

        <div class="info">
            <p>
                {{ item.modelo.nome }} - {{ item.ano }}
            </p>

            <p>
                R$ {{ item.preco }}
            </p>

            <p>
                {{ item.cor.descricao }}
            </p>
        </div>

        <button class="deletar" v-if="deletar" @click="$emit('deletar', item.id)">Deletar</button>
    </div>
</template>

<style scoped>
    .card {
        width: 300px;
        padding: 10px 0;
        box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
        border-radius: 10px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 10px;
    }

    .info {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 20px;
    }

    .deletar {
        background-color: transparent;
        width: 60%;
        margin: 0 10px;
        margin: auto;
        cursor: pointer;
        border-radius: 20px;
        background-color: red;
        padding: 10px 20px;
        border: none;
        color: white;
    }   
</style>    