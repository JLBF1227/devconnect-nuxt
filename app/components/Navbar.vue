<template>
  <header class="navbar bg-base-100 shadow-md px-6">
    <div class="flex-1">
      <NuxtLink
        to="/"
        class="text-2xl font-bold text-primary"
      >
        DevConnect
      </NuxtLink>
    </div>

    <nav class="flex gap-2">
      <NuxtLink
        to="/"
        class="btn btn-ghost"
      >
        Início
      </NuxtLink>

      <NuxtLink
        to="/cadastro"
        class="btn btn-primary"
      >
        Cadastro
      </NuxtLink>
    </nav>
  </header>
</template>