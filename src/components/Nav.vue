<template>
  <nav class="navbar navbar-expand-md navbar-dark bg-dark mb-4">
    <div class="container-fluid">
      <router-link to="/" class="navbar-brand" href="#">Início</router-link>

      <div>
        <ul class="navbar-nav me-auto mb-2 mb-md-0" v-if="!auth">
          <li class="nav-item">
            <router-link to="/login" class="nav-link active">Login</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/registrar" class="nav-link active">Cadastre-se</router-link>
          </li>
        </ul>

        <ul class="navbar-nav me-auto mb-2 mb-md-0" v-if="auth">
          <li class="nav-item">
            <router-link to="/atualizar" class="nav-link active">Atualizar dados</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/login" class="nav-link" @click="logout">Sair</router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script lang="ts">
import {useStore} from "vuex";
import {computed} from "vue";

export default {
  name: "Nav",
  setup() {
    const store = useStore();

    const auth = computed(() => store.state.authenticated)

    const logout = async () => {
      await fetch('http://localhost:8000/api/logout', {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        credentials: 'include'
      });
    }

    return {
      auth,
      logout
    }
  }
}
</script>