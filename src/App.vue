<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header>
    <div>
      <nav>
        <RouterLink to="/">Home</RouterLink>
      </nav>
    </div>
  </header>
  <main>
    <h1 class="text-3xl font-bold underline text-center">Hello world!</h1>
  </main>
  <RouterView />
</template>
