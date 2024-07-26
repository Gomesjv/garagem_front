<script setup>
defineProps(["item"])
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
    </div>
</template>

<style scoped>
    .card {
        width: 300px;
        padding: 10px 0;
        box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
        border-radius: 10px;
    }

    .info {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 20px;
    }
</style>    