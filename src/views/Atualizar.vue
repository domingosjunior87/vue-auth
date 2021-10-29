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
            <input
                v-model="data.data_nascimento"
                class="form-control"
                id="nascimento"
                v-maska="'##/##/####'"
                placeholder="  /  /"
                required
            >
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
            <input v-model="data.cpf" class="form-control" id="cpf" v-maska="'###.###.###-##'" required>
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
            <input
                v-model="data.telefone"
                class="form-control"
                id="telefone"
                v-maska="'(##) ####-####'"
                placeholder="(99) 9999-9999"
            >
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <label for="celular" class="form-label">Celular*</label>
            <input
                v-model="data.celular"
                class="form-control"
                id="celular"
                v-maska="'(##) #####-####'"
                placeholder="(99) 99999-9999"
                required
            >
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
            <input v-model="data.cep" class="form-control" id="cep" v-maska="'#####-###'" required>
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

      <button class="w-100 btn btn-lg btn-primary" type="submit">Atualizar</button>
    </div> <!-- .container -->
  </form>
</template>

<script lang="ts">
import {onMounted, reactive} from "vue";
import {useRouter} from "vue-router";

export default {
  name: "Atualizar",
  setup() {
    let data = reactive({
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
      email: ''
    });

    const router = useRouter();

    const submit = async () => {
      let dados = data;

      dados.cpf = dados.cpf.replaceAll('.','');
      dados.cpf = dados.cpf.replace('-','');

      dados.cep = dados.cep.replace('-','');

      dados.celular = dados.celular.replace('(','');
      dados.celular = dados.celular.replace(')','');
      dados.celular = dados.celular.replace(' ','');
      dados.celular = dados.celular.replace('-','');

      if (dados.telefone) {
          dados.telefone = dados.telefone.replace('(','');
          dados.telefone = dados.telefone.replace(')','');
          dados.telefone = dados.telefone.replace(' ','');
          dados.telefone = dados.telefone.replace('-','');
      }

      await fetch("http://localhost:8000/api/user", {
        method: 'PUT',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(dados),
        credentials: 'include'
      })
          .then(async response => {
            const resposta = await response.json();

            if (!response.ok) {
              const error = (resposta && resposta.message) || response.statusText;
              return Promise.reject(error);
            }

            await router.push('/');
          })
          .catch(error => {
            alert(error);
          });
    }

    onMounted(async () => {
      try {
        const response = await fetch('http://localhost:8000/api/user', {
          headers: {'Content-Type': 'application/json'},
          credentials: 'include'
        });

        let dados = await response.json();

        data.nome = dados.nome;
        data.data_nascimento = dados.data_nascimento;
        data.sexo = dados.sexo;
        data.cpf = dados.cpf;
        data.rg = dados.rg;
        data.telefone = dados.telefone;
        data.celular = dados.celular;
        data.identificacao = dados.identificacao;
        data.cep = dados.cep;
        data.logradouro = dados.logradouro;
        data.numero = dados.numero;
        data.complemento = dados.complemento;
        data.bairro = dados.bairro;
        data.cidade = dados.cidade;
        data.referencia = dados.referencia;
        data.email = dados.email;


      } catch (e) {
        alert('Não foi possível obter os dados');
        console.log(e);
      }
    });

    return {
      data,
      submit
    }
  }
}
</script>