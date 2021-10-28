<template>
  <form @submit.prevent="submit">
    <div class="container">
      <h1 class="h3 mb-3 fw-normal">Efetue seu cadastro</h1>

      <div class="row">
        <div class="col">
          <div class="mb-3">
            <label for="nome" class="form-label">Nome Completo*</label>
            <input v-model="data.nome" class="form-control" id="nome" required>
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <div class="mb-3">
            <label for="nascimento" class="form-label">Data de Nascimento*</label>
            <input v-model="data.data_nascimento" class="form-control" id="nascimento" required>
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <label for="sexo" class="form-label">Sexo</label>
            <select v-model="data.sexo" id="sexo" class="form-select">
              <option value="M">Masculino</option>
              <option value="F">Feminino</option>
              <option value="O">Outro</option>
            </select>
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <div class="mb-3">
            <label for="cpf" class="form-label">CPF*</label>
            <input v-model="data.cpf" class="form-control" id="cpf" required>
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <label for="rg" class="form-label">RG</label>
            <input v-model="data.rg" class="form-control" id="rg">
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <div class="mb-3">
            <label for="telefone" class="form-label">Telefone</label>
            <input v-model="data.telefone" class="form-control" id="telefone">
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <label for="celular" class="form-label">Celular*</label>
            <input v-model="data.celular" class="form-control" id="celular" required>
          </div>
        </div>
      </div>

      <hr />
      <h2 class="h4 fw-normal">Endereço</h2>

      <div class="row">
        <div class="col">
          <div class="mb-3">
            <label for="identificacao" class="form-label">Identificação*</label>
            <input v-model="data.identificacao" class="form-control" id="identificacao" required>
            <div id="emailHelp" class="form-text">Ex: Escritório, Casa, Sítio, etc</div>
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <label for="cep" class="form-label">CEP*</label>
            <input v-model="data.cep" class="form-control" id="cep" required>
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <div class="mb-3">
            <label for="logradouro" class="form-label">Endereço*</label>
            <input v-model="data.logradouro" class="form-control" id="logradouro" required>
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <label for="numero" class="form-label">Número*</label>
            <input v-model="data.numero" class="form-control" id="numero" required>
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <div class="mb-3">
            <label for="complemento" class="form-label">Complemento</label>
            <input v-model="data.complemento" class="form-control" id="complemento">
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <div class="mb-3">
            <label for="bairro" class="form-label">Bairro*</label>
            <input v-model="data.bairro" class="form-control" id="bairro" required>
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <label for="cidade" class="form-label">Cidade*</label>
            <input v-model="data.cidade" class="form-control" id="cidade" required>
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <div class="mb-3">
            <label for="uf" class="form-label">Estado</label>
            <input class="form-control" id="uf">
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <label for="referencia" class="form-label">Referência</label>
            <input v-model="data.referencia" class="form-control" id="referencia">
          </div>
        </div>
      </div>

      <hr />

      <div class="row">
        <div class="col">
          <div class="mb-3">
            <label for="email" class="form-label">Email*</label>
            <input v-model="data.email" type="email" class="form-control" id="email" required>
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <div class="mb-3">
            <label for="password" class="form-label">Senha*</label>
            <input v-model="data.password" type="password" class="form-control" id="password" required>
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <label for="confirm_password" class="form-label">Confirme a senha*</label>
            <input v-model="data.confirm_password" type="password" class="form-control" id="confirm_password" required>
          </div>
        </div>
      </div>

      <button class="w-100 btn btn-lg btn-primary" type="submit">Cadastrar</button>
    </div> <!-- .container -->
  </form>
</template>

<script lang="ts">
import {reactive} from "vue";
import {useRouter} from "vue-router";

export default {
  name: "Register",
  setup() {
    const data = reactive({
      nome: '',
      data_nascimento: '',
      sexo: '',
      cpf: '',
      rg: '',
      telefone: '',
      celular: '',
      identificacao: '',
      cep: '',
      logradouro: '',
      numero: '',
      complemento: '',
      bairro: '',
      cidade: '',
      referencia: '',
      email: '',
      password: '',
      confirm_password: ''
    });

    const router = useRouter();

    const submit = async () => {
      await fetch('http://localhost:8000/api/register', {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(data)
      });

      await router.push('/login');
    }

    return {
      data,
      submit
    }
  }
}
</script>