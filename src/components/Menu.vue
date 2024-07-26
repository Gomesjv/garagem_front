<script setup>
const links = [
    {
        path: '/',
        name: 'Home',
    },
    {
        path: "/categorias",
        name: "categorias",
    },
    {
        path: "/cores",
        name: "cores",
    },
    {
        path: "/acessorios",
        name: "acessorios",
    },
    {
        path: "/marcas",
        name: "marcas",
    },
    {
        path: "/veiculos",
        name: "veiculos"
    },
    {
        path: "/modelos",
        name: "modelos"
    },
]
</script>

<template>
    <section>
        <div class="link" v-for="link in links">
            <router-link :to="link.path" @click="$emit('close')">{{ link.name }}</router-link>
        </div>
    </section>
</template>

<style scoped>
    section {
        width: 100%;
        position: absolute;
        left: 0;
        top: 40px;
        height: 50px;
        background-color: #ddd;
        display: flex;
        gap: 20px;
        align-items: center;
        justify-content: space-around;
    }

    .link a {
        text-decoration: none;
        color: black;
        text-transform: uppercase;
        font-weight: bold;
    }
</style>