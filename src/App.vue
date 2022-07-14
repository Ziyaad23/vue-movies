<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header>
    <div>
      <nav>
        <RouterLink to="/">
          <h1
            class="flex items-center justify-center px-2.5 py-4 bg-green-400 text-white text-2xl font-bold font-mono drop-shadow">
            OMDb Movies
          </h1>
        </RouterLink>
      </nav>
    </div>
  </header>
  <main>
    <RouterView />
  </main>
</template>
