<script setup>
import { ref, watch } from 'vue'

const user = ref({
  name: '',
  surname: '',
  email: '',
  password: '',
  city: '',
  state: '',
  zip: '',
  hobbies: [],
  preferredLanguage: '',
  bio: ''
})

const states = [
  { uf: 'AC', name: 'Acre' },
  { uf: 'AL', name: 'Alagoas' },
  { uf: 'AP', name: 'Amapá' },
  { uf: 'AM', name: 'Amazonas' },
  { uf: 'BA', name: 'Bahia' },
  { uf: 'CE', name: 'Ceará' },
  { uf: 'DF', name: 'Distrito Federal' },
  { uf: 'ES', name: 'Espírito Santo' },
  { uf: 'GO', name: 'Goiás' },
  { uf: 'MA', name: 'Maranhão' },
  { uf: 'MT', name: 'Mato Grosso' },
  { uf: 'MS', name: 'Mato Grosso do Sul' },
  { uf: 'MG', name: 'Minas Gerais' },
  { uf: 'PA', name: 'Pará' },
  { uf: 'PB', name: 'Paraíba' },
  { uf: 'PR', name: 'Paraná' },
  { uf: 'PE', name: 'Pernambuco' },
  { uf: 'PI', name: 'Piauí' },
  { uf: 'RJ', name: 'Rio de Janeiro' },
  { uf: 'RN', name: 'Rio Grande do Norte' },
  { uf: 'RS', name: 'Rio Grande do Sul' },
  { uf: 'RO', name: 'Rondônia' },
  { uf: 'RR', name: 'Roraima' },
  { uf: 'SC', name: 'Santa Catarina' },
  { uf: 'SP', name: 'São Paulo' },
  { uf: 'SE', name: 'Sergipe' },
  { uf: 'TO', name: 'Tocantins' }
]

const senha = ref('')
const confirmarSenha = ref('')
const senhasDiferentes = ref(false)
const senhaCurta = ref(false)

watch(senha, (novaSenha) => {
  senhaCurta.value = novaSenha.length < 4
})

watch([senha, confirmarSenha], ([novaSenha, novaConfirmacao]) => {
  senhasDiferentes.value = novaSenha !== novaConfirmacao
})

const mostrarPerfil = ref(false)

function salvarPerfil() {
  if (!senhaCurta.value && !senhasDiferentes.value) {
    mostrarPerfil.value = true
  } else {
    if (senhaCurta.value) {
      alert('A senha deve ter no mínimo 4 caracteres.')
    }
    if (senhasDiferentes.value) {
      alert('As senhas não coincidem. Por favor, verifique.')
    }
  }
}


</script>

<template>
  <div class="container">
    <main>
      <h1>Formulário 1</h1>
      <transition name="form" mode="out-in">
        <section v-if="mostrarPerfil">
          <div class="mt-5 mb-3">
            <p v-for="(value, key) of user" :key="key">{{ key }}: {{ value }}</p>
          </div>
          <button class="btn btn-info" @click="mostrarPerfil = false">Esconder</button>
        </section>
        <form v-else class="row g-3 was-validated" @submit.prevent="salvarPerfil()" validate>
          <div>
            <label for="nameField" class="form-label">Nome </label>
            <input type="text" class="form-control" id="nameField" v-model="user.name" placeholder="Digite seu nome"
              required />
          </div>
          <div>
            <label for="surnameField" class="form-label">Sobrenome </label>
            <input type="text" class="form-control" id="surnameField" v-model="user.surname"
              placeholder="Digite seu sobrenome" required />
          </div>
          <div>
            <label for="emailField" class="form-label">E-mail </label>
            <div class="input-group">
              <input type="email" class="form-control" id="emailField" aria-describedby="emailFieldPrepend"
                v-model="user.email" placeholder="email@gmail.com" required />
            </div>
          </div>
          <div>
            <label for="passwordField" class="form-label">Senha</label>
            <input type="password" v-model="senha" placeholder="Senha" required>
            <span v-if="senhaCurta">A senha deve ter no mínimo 4 caracteres.</span>
          </div>
          <div>
            <label for="confirmPasswordField" class="form-label">Confirmar Senha</label>
            <input type="password" v-model="confirmarSenha" placeholder="Confirmar Senha" required>
            <span v-if="senhasDiferentes">As senhas não coincidem.</span>
          </div>
          <div>
            <label for="cityField" class="form-label">Cidade </label>
            <input type="text" class="form-control" id="cityField" v-model="user.city" placeholder="Informe a cidade"
              required />
          </div>
          <div>
            <label for="stateField" class="form-label">Estado </label>
            <select class="form-select" id="stateField" v-model="user.state">
              <option selected disabled value="">Selecionar</option>
              <option v-for="state of states" :key="state.uf" :value="state.uf">
                {{ state.name }}
              </option>
            </select>
          </div>
          <div>
            <label for="zipField" class="form-label">CEP </label>
            <input type="text" class="form-control" id="zipField" v-model="user.zip" placeholder="Digite seu CEP"
              required />
          </div>
          <div>
            <p>Hobbies</p>
            <input class="ms-3 me-1" type="checkbox" id="hobbiesField" value="esportes" v-model="user.hobbies" />
            <label for="hobbiesField"> Esportes </label>
            <input class="ms-3 me-1" type="checkbox" id="hobbiesField" value="música" v-model="user.hobbies" />
            <label for="hobbiesField"> Jogos </label>
            <input class="ms-3 me-1" type="checkbox" id="hobbiesField" value="viagens" v-model="user.hobbies" />
            <label for="hobbiesField"> Leitura </label>
            <input class="ms-3 me-1" type="checkbox" id="hobbiesField" value="leitura" v-model="user.hobbies" />
            <label for="hobbiesField"> Estudos </label>
          </div>
          <div>
            <p>Linguagem preferida </p>
            <input class="ms-3 me-1" type="radio" v-model="user.preferredLanguage" value="C" id="langC" />
            <label for="langC"> C </label>
            <input class="ms-3 me-1" type="radio" v-model="user.preferredLanguage" value="Java" id="langJava" />
            <label for="langJava"> Java </label>
            <input class="ms-3 me-1" type="radio" v-model="user.preferredLanguage" value="Python" id="langPython" />
            <label for="langPython"> Python </label>
            <input class="ms-3 me-1" type="radio" v-model="user.preferredLanguage" value="Javascript" id="langJs" />
            <label for="langJs"> JavaScript </label>
          </div>
          <div>
            <label for="nameField" class="form-label">Biografia </label>
            <input type="text" class="form-control" id="nameField" v-model="user.bio" placeholder="Breve biografia"
              required />
          </div>
          <div>
            <button class="btn btn-primary" type="submit">Enviar</button>
          </div>
        </form>
      </transition>
    </main>
  </div>
</template>

<style scoped>
body {
  background-color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

.container {
  background-color: #f2f2f2;
  border-radius: 15px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  width: 50%;
  max-width: 600px;
  margin: auto;
}

.mt-5 {
  margin-top: 3rem;

}

.mb-3 {
  margin-bottom: 1rem;

}

.btn {
  background-color: #17a2b8;
  border: none;
  border-radius: 5px;
  padding: 10px;
  color: white;
  cursor: pointer;
  display: inline-block;
  text-align: center;
}

.btn-info {
  background-color: #17a2b8;

}

.btn-info:hover {
  background-color: #138496;

}

input[type="text"],
input[type="email"],
input[type="password"],
select.form-select {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  width: 100%;
}

.input-group-text {
  background-color: #eee;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
}

.input-group {
  display: flex;
}

input[type="checkbox"],
input[type="radio"] {
  margin-right: 5px;
}

label {
  margin-bottom: .5rem;
}

.form-label {
  display: block;
}

.form-control {
  display: block;
  width: 100%;
  padding: .375rem .75rem;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  color: #212529;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ced4da;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  border-radius: .25rem;
}

.form-select {
  display: inline-block;
  width: 100%;
  padding: .375rem 2.25rem .375rem .75rem;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  color: #212529;
  background-color: #fff;
  background-repeat: no-repeat;
  background-position: right .75rem center;
  background-size: 16px 12px;
  border: 1px solid #ced4da;
  border-radius: .25rem;
}

[type="submit"] {
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 10px;
  cursor: pointer;
}

[type="submit"]:hover {
  background-color: #218838;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 10px;
  cursor: pointer;

}
</style>