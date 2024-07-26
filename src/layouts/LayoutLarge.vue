<script setup>
import HeaderLarge from '@/components/templates/header/HeaderLarge.vue';
import { RouterView } from 'vue-router';
</script>

<template>
    <HeaderLarge></HeaderLarge>

    <main>
        <RouterView></RouterView>
    </main>
</template>