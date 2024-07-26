<script setup>
import HeaderSmall from '@/components/templates/header/HeaderSmall.vue';
import { RouterView } from 'vue-router';
</script>

<template>
    <HeaderSmall></HeaderSmall>
    <main>
        <RouterView></RouterView>
    </main>
</template>