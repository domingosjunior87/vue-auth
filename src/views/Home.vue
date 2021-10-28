<template>
  <div class="center">{{ message }}</div>
</template>

<script lang="ts">
import {onMounted, ref} from 'vue'
import {useStore} from 'vuex'

export default {
  name: "Home",
  setup() {
    const message = ref('Bem vindo, faça o login ou cadastre-se!');

    const store = useStore();

    onMounted(async () => {
      try {
        const response = await fetch('http://localhost:8000/api/user', {
          headers: {'Content-Type': 'application/json'},
          credentials: 'include'
        });

        const content = await response.json();

        message.value = `Bem-vindo ${content.nome}`;

        await store.dispatch('setAuth', true);
      } catch (e) {
        await store.dispatch('setAuth', false);
      }
    });

    return {
      message
    }
  }
}
</script>

<style scoped>
  .center {
    text-align: center;
  }
</style>