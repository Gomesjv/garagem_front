<script setup>
import { onMounted, ref } from 'vue';
import { PassageUser } from '@passageidentity/passage-elements/passage-user';
import { useAuthStore } from '@/stores/auth';
import VeiculosApi from '@/api/veiculos';
const veiculosApi = new VeiculosApi();
import VeiculoCard from '@/components/VeiculoCard.vue';

const veiculos = ref()
const authStore = useAuthStore();

const getUserInfo = async () => {
  try {
    const authToken = localStorage.getItem('psg_auth_token');
    const passageUser = new PassageUser(authToken);
    const user = await passageUser.userInfo(authToken);
    if (user) {
      await authStore.setToken(authToken);
    } else {
      authStore.unsetToken();
    }
  } catch (error) {
    authStore.unsetToken();
  }
};

onMounted(async () => {
  veiculos.value = await veiculosApi.buscarTodosOsVeiculos()
  getUserInfo();
});
</script>

<template>
  <section class="veiculos">
    <VeiculoCard v-for="veiculo in veiculos" :item="veiculo" :deletar="false"></VeiculoCard>
  </section>
</template>

<style scoped>
.veiculos {
        display: flex;
        flex-wrap: wrap;
        padding: 10px 20px;
        align-items: center;
        justify-content: space-around;
    }
</style>