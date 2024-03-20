<script setup>
import { ref } from 'vue'

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

const mostrarPerfil = ref(false)

function salvarPerfil() {
  mostrarPerfil.value = true
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
            <img v-if="user.avatar" class="avatar" :src="user.avatar" />
          </div>
          <button class="btn btn-info" @click="mostrarPerfil = false">Esconder</button>
        </section>
        <form v-else class="row g-3 was-validated" @submit.prevent="salvarPerfil()" validate>
          <div>
            <label for="nameField" class="form-label">Nome: </label>
            <input type="text" class="form-control" id="nameField" v-model="user.name" placeholder="Digite seu nome"
              required />
          </div>
          <div>
            <label for="surnameField" class="form-label">Sobrenome: </label>
            <input type="text" class="form-control" id="surnameField" v-model="user.surname"
              placeholder="Digite seu sobrenome" required />
          </div>
          <div>
            <label for="emailField" class="form-label">E-mail: </label>
            <div class="input-group">
              <span class="input-group-text" id="emailFieldPrepend"></span>
              <input type="email" class="form-control" id="emailField" aria-describedby="emailFieldPrepend"
                v-model="user.email" placeholder="email@gmail.com" required />
            </div>
          </div>
          <div>
            <label for="passwordField" class="form-label">Senha: </label>
            <input type="password" name="password" id="passwordField" placeholder="Senha" required>
            <input type="password" name="passwordV" id="passwordField" placeholder="Confirmar Senha" required>
          </div>
          <div>
            <label for="cityField" class="form-label">Cidade: </label>
            <input type="text" class="form-control" id="cityField" v-model="user.city" placeholder="Informe a cidade" required />
          </div>
          <div>
            <label for="stateField" class="form-label">Estado: </label>
            <select class="form-select" id="stateField" v-model="user.state">
              <option selected disabled value="" placeholder="Selecionar"></option>
              <option v-for="state of states" :key="state.uf" :value="state.uf">
                {{ state.name }}
              </option>
            </select>
          </div>
          <div>
            <label for="zipField" class="form-label">CEP</label>
            <input type="text" class="form-control" id="zipField" v-model="user.zip" />
          </div>
          <div>
            <p>Hobbies</p>
            <input class="ms-3 me-1" type="checkbox" id="hobbiesField" value="esportes" v-model="user.hobbies" />
            <label for="hobbiesField">Esportes</label>
            <input class="ms-3 me-1" type="checkbox" id="hobbiesField" value="música" v-model="user.hobbies" />
            <label for="hobbiesField">Jogos</label>
            <input class="ms-3 me-1" type="checkbox" id="hobbiesField" value="viagens" v-model="user.hobbies" />
            <label for="hobbiesField">Leitura</label>
            <input class="ms-3 me-1" type="checkbox" id="hobbiesField" value="leitura" v-model="user.hobbies" />
            <label for="hobbiesField">Estudos</label>
          </div>
          <div>
            <p>Linguagem preferida</p>
            <input class="ms-3 me-1" type="radio" v-model="user.preferredLanguage" value="C" id="langC" />
            <label for="langC">C</label>
            <input class="ms-3 me-1" type="radio" v-model="user.preferredLanguage" value="Java" id="langJava" />
            <label for="langJava">Java</label>
            <input class="ms-3 me-1" type="radio" v-model="user.preferredLanguage" value="Python" id="langPython" />
            <label for="langPython">Python</label>
            <input class="ms-3 me-1" type="radio" v-model="user.preferredLanguage" value="Javascript" id="langJs" />
            <label for="langJs">JavaScript</label>
          </div>
          <div>
            <label for="nameField" class="form-label">Biografia</label>
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

<style scoped></style>