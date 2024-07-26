<script setup>
import { ref } from 'vue';
import Menu from '@/components/Menu.vue';
import { useAuthStore } from '@/stores/auth';
const authStore = useAuthStore();

const menu = ref(false)
</script>

<template>
    <header>
        <div class="menu" @click="menu = !menu">
            <i class="mdi mdi-menu"></i>
        </div>

        <img src="/logo.png" alt="logo" width="40px">

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

    <Menu v-if="menu" @close="menu = false"></Menu>
</template>

<style scoped>
    header {
        position: relative;
        display: flex;
        height: 40px;
        align-items: center;
        justify-content: space-between;
        padding: 0px 10px;
        box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
    }

    .menu {
        cursor: pointer;
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