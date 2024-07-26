<script setup>
import HeaderMedium from '@/components/templates/header/HeaderMedium.vue';
import { RouterView } from 'vue-router';
</script>

<template>
    <HeaderMedium></HeaderMedium>
    <main>
        <RouterView></RouterView>
    </main>
</template>