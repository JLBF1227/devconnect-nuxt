<script setup lang="ts">
import { computed, reactive, ref } from 'vue'

const formulario = reactive({
  nome: '',
  email: '',
  curso: '',
  semestre: '',
  interesses: [] as string[],
  bio: ''
})

const erros = reactive({
  nome: '',
  email: '',
  curso: '',
  semestre: '',
  interesses: ''
})

const mensagemSucesso = ref(false)

const limiteBio = 200

const caracteresRestantes = computed(() => {
  return limiteBio - formulario.bio.length
})

function validarEmail(email: string) {
  const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  return regex.test(email)
}

function limparErros() {
  erros.nome = ''
  erros.email = ''
  erros.curso = ''
  erros.semestre = ''
  erros.interesses = ''
}

function validarFormulario() {
  limparErros()

  let formularioValido = true

  if (!formulario.nome.trim()) {
    erros.nome = 'O nome completo é obrigatório.'
    formularioValido = false
  }

  if (!formulario.email.trim()) {
    erros.email = 'O e-mail é obrigatório.'
    formularioValido = false
  } else if (!validarEmail(formulario.email)) {
    erros.email = 'Digite um e-mail válido.'
    formularioValido = false
  }

  if (!formulario.curso) {
    erros.curso = 'Selecione um curso ou área de atuação.'
    formularioValido = false
  }

  if (!formulario.semestre) {
    erros.semestre = 'Informe o semestre/período.'
    formularioValido = false
  }

  if (formulario.interesses.length === 0) {
    erros.interesses = 'Selecione pelo menos um interesse.'
    formularioValido = false
  }

  return formularioValido
}

function limparFormulario() {
  formulario.nome = ''
  formulario.email = ''
  formulario.curso = ''
  formulario.semestre = ''
  formulario.interesses = []
  formulario.bio = ''
}

function enviarFormulario() {
  mensagemSucesso.value = false

  if (!validarFormulario()) {
    return
  }

  console.log('Dados do novo membro:')
  console.log({
    nome: formulario.nome,
    email: formulario.email,
    curso: formulario.curso,
    semestre: formulario.semestre,
    interesses: [...formulario.interesses],
    bio: formulario.bio
  })

  mensagemSucesso.value = true

  limparFormulario()

  setTimeout(() => {
    mensagemSucesso.value = false
  }, 5000)
}
</script>

<template>
  <main class="min-h-[calc(100vh-64px)] px-4 py-12 sm:px-6">

    <div class="mx-auto max-w-3xl">

      <div class="mb-8 text-center">
        <h1 class="text-4xl font-bold">
          Cadastro de Membro
        </h1>

        <p class="mt-3 opacity-70">
          Preencha seus dados para fazer parte do DevConnect.
        </p>
      </div>

      <div
        v-if="mensagemSucesso"
        class="alert alert-success mb-6"
      >
        <span>
          Cadastro realizado com sucesso!
        </span>
      </div>

      <div class="card bg-base-100 shadow-xl">
        <div class="card-body">

          <h2 class="card-title mb-2 text-2xl">
            Novo membro
          </h2>

          <p class="mb-6 opacity-70">
            Informe seus dados pessoais, acadêmicos e interesses.
          </p>

          <form
            class="space-y-6"
            @submit.prevent="enviarFormulario"
          >

            <!-- Nome completo -->
            <div>
              <label
                for="nome"
                class="label"
              >
                <span class="label-text font-semibold">
                  Nome completo
                </span>
              </label>

              <input
                id="nome"
                v-model="formulario.nome"
                type="text"
                placeholder="Digite seu nome completo"
                class="input input-bordered w-full"
              >

              <p
                v-if="erros.nome"
                class="mt-1 text-sm text-error"
              >
                {{ erros.nome }}
              </p>
            </div>

            <!-- E-mail -->
            <div>
              <label
                for="email"
                class="label"
              >
                <span class="label-text font-semibold">
                  E-mail
                </span>
              </label>

              <input
                id="email"
                v-model="formulario.email"
                type="email"
                placeholder="exemplo@email.com"
                class="input input-bordered w-full"
              >

              <p
                v-if="erros.email"
                class="mt-1 text-sm text-error"
              >
                {{ erros.email }}
              </p>
            </div>

            <!-- Curso -->
            <div>
              <label
                for="curso"
                class="label"
              >
                <span class="label-text font-semibold">
                  Curso / Área de atuação
                </span>
              </label>

              <select
                id="curso"
                v-model="formulario.curso"
                class="select select-bordered w-full"
              >
                <option
                  value=""
                  disabled
                >
                  Selecione uma opção
                </option>

                <option value="Engenharia de Software">
                  Engenharia de Software
                </option>

                <option value="Ciência da Computação">
                  Ciência da Computação
                </option>

                <option value="Sistemas de Informação">
                  Sistemas de Informação
                </option>

                <option value="Análise e Desenvolvimento de Sistemas">
                  Análise e Desenvolvimento de Sistemas
                </option>

                <option value="Design">
                  Design
                </option>

                <option value="Outra">
                  Outra
                </option>
              </select>

              <p
                v-if="erros.curso"
                class="mt-1 text-sm text-error"
              >
                {{ erros.curso }}
              </p>
            </div>

            <!-- Semestre -->
            <div>
              <label
                for="semestre"
                class="label"
              >
                <span class="label-text font-semibold">
                  Semestre / Período
                </span>
              </label>

              <select
                id="semestre"
                v-model="formulario.semestre"
                class="select select-bordered w-full"
              >
                <option
                  value=""
                  disabled
                >
                  Selecione o período
                </option>

                <option
                  v-for="periodo in 10"
                  :key="periodo"
                  :value="periodo"
                >
                  {{ periodo }}º período
                </option>
              </select>

              <p
                v-if="erros.semestre"
                class="mt-1 text-sm text-error"
              >
                {{ erros.semestre }}
              </p>
            </div>

            <!-- Interesses -->
            <div>
              <span class="mb-3 block font-semibold">
                Interesses / Habilidades
              </span>

              <div class="grid gap-3 sm:grid-cols-2">

                <label class="flex cursor-pointer items-center gap-3">
                  <input
                    v-model="formulario.interesses"
                    type="checkbox"
                    value="Front-end"
                    class="checkbox checkbox-primary"
                  >
                  <span>Front-end</span>
                </label>

                <label class="flex cursor-pointer items-center gap-3">
                  <input
                    v-model="formulario.interesses"
                    type="checkbox"
                    value="Back-end"
                    class="checkbox checkbox-primary"
                  >
                  <span>Back-end</span>
                </label>

                <label class="flex cursor-pointer items-center gap-3">
                  <input
                    v-model="formulario.interesses"
                    type="checkbox"
                    value="Mobile"
                    class="checkbox checkbox-primary"
                  >
                  <span>Mobile</span>
                </label>

                <label class="flex cursor-pointer items-center gap-3">
                  <input
                    v-model="formulario.interesses"
                    type="checkbox"
                    value="UI/UX"
                    class="checkbox checkbox-primary"
                  >
                  <span>UI/UX</span>
                </label>

                <label class="flex cursor-pointer items-center gap-3">
                  <input
                    v-model="formulario.interesses"
                    type="checkbox"
                    value="Banco de Dados"
                    class="checkbox checkbox-primary"
                  >
                  <span>Banco de Dados</span>
                </label>

                <label class="flex cursor-pointer items-center gap-3">
                  <input
                    v-model="formulario.interesses"
                    type="checkbox"
                    value="DevOps"
                    class="checkbox checkbox-primary"
                  >
                  <span>DevOps</span>
                </label>

              </div>

              <p
                v-if="erros.interesses"
                class="mt-2 text-sm text-error"
              >
                {{ erros.interesses }}
              </p>
            </div>

            <!-- Bio -->
            <div>
              <label
                for="bio"
                class="label"
              >
                <span class="label-text font-semibold">
                  Mensagem / Bio curta
                </span>
              </label>

              <textarea
                id="bio"
                v-model="formulario.bio"
                :maxlength="limiteBio"
                class="textarea textarea-bordered h-32 w-full resize-none"
                placeholder="Conte um pouco sobre você..."
              />

              <div class="mt-1 text-right text-sm opacity-60">
                {{ formulario.bio.length }} / {{ limiteBio }}
                caracteres
              </div>

              <div class="text-right text-xs opacity-50">
                Restantes: {{ caracteresRestantes }}
              </div>
            </div>

            <!-- Botão -->
            <div class="card-actions justify-end pt-4">
              <button
                type="submit"
                class="btn btn-primary w-full sm:w-auto"
              >
                Cadastrar membro
              </button>
            </div>

          </form>

        </div>
      </div>

    </div>

  </main>
</template>