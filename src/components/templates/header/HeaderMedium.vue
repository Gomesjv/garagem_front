<script setup>
import { useAuthStore } from '@/stores/auth';
const authStore = useAuthStore();
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
    <header>
        <img src="/logo.png" alt="logo" width="40px">

        <div class="links">
            <p class="link" v-for="link in links">
                <router-link :to="link.path">{{ link.name }}</router-link>
            </p>
        </div>

        <div >
            <div v-if="authStore.loggedIn" class="logout">
                {{ authStore.user.email }}
                <button class="btn-logout">
                <router-link to="/logout">
                    <i class="mdi mdi-exit-to-app mdi-24px " style="color: black;"></i>
                </router-link>
            </button>
            </div>
            <button class="btn-login" v-else>
                <router-link to="/login">
                    Login
                </router-link>
            </button>
        </div>
    </header>
</template>

<style scoped>
    header {
        display: flex;
        height: 40px;
        align-items: center;
        justify-content: space-between;
        padding: 0px 10px;
        box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
    }

    .links {
        display: flex;
        gap: 10px;
    }

    .link {
        text-transform: uppercase;
    }

    .link a {
        text-decoration: none;
        color: black;
        font-weight: bold;
    }

    .btn-login {
        background-color: black;
        border: none;
        border-radius: 10px;
        padding: 5px 20px;
        color: white;
        text-transform: uppercase;
        font-weight: bold;
    }

    .btn-login a {
        text-decoration: none;
        color: white;
        font-weight: bold;
    }

    .logout {
        display: flex;
        align-items: center;
    }

    .btn-logout {
        background-color: transparent;
        border: none;
        color: black;
    }
</style>