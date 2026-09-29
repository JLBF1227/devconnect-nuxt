<template>
  <main class="flex min-h-[calc(100vh-64px)] items-center justify-center px-6">
    <section class="max-w-4xl text-center">
      <div class="mb-4">
        <span class="badge badge-primary badge-lg">
          Comunidade Acadêmica
        </span>
      </div>

      <h1 class="mb-6 text-5xl font-bold">
        Conecte-se com quem também
        <span class="text-primary">
          desenvolve o futuro.
        </span>
      </h1>

      <p class="mx-auto mb-8 max-w-2xl text-lg opacity-70">
        O DevConnect é um espaço para estudantes e profissionais
        compartilharem seus interesses, habilidades e áreas de atuação.
      </p>

      <div class="flex justify-center gap-4">
        <NuxtLink
          to="/cadastro"
          class="btn btn-primary btn-lg"
        >
          Cadastrar membro
        </NuxtLink>

        <a
          href="#sobre"
          class="btn btn-outline btn-lg"
        >
          Saiba mais
        </a>
      </div>
    </section>
  </main>

  <section
    id="sobre"
    class="bg-base-100 px-6 py-20"
  >
    <div class="mx-auto max-w-5xl">
      <h2 class="mb-10 text-center text-3xl font-bold">
        Sobre o DevConnect
      </h2>

      <div class="grid gap-6 md:grid-cols-3">

        <div class="card bg-base-200 shadow-md">
          <div class="card-body">
            <h3 class="card-title">
              Conecte-se
            </h3>

            <p>
              Encontre pessoas com interesses e áreas de atuação semelhantes.
            </p>
          </div>
        </div>

        <div class="card bg-base-200 shadow-md">
          <div class="card-body">
            <h3 class="card-title">
              Compartilhe
            </h3>

            <p>
              Apresente suas habilidades, experiências e interesses.
            </p>
          </div>
        </div>

        <div class="card bg-base-200 shadow-md">
          <div class="card-body">
            <h3 class="card-title">
              Aprenda
            </h3>

            <p>
              Descubra novas áreas da tecnologia e conheça outros estudantes.
            </p>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>