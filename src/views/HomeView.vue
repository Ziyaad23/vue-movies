<template>
  <section class="text-gray-800 text-center lg:text-left">
    <router-link to=/movie/tt0096895>
      <div class="relative overflow-hidden bg-no-repeat bg-cover" style="
          background-position: 50%;
          background-image: url('https://images.unsplash.com/photo-1583156340160-7867f31285d5?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&q=100');
          height: 500px;
        ">
        <div class="absolute top-0 right-0 bottom-0 left-0 w-full h-full overflow-hidden bg-fixed"
          style="background-color: rgba(0, 0, 0, 0.75)">
          <div class="flex justify-center items-center h-full">
            <div class="text-center text-white px-6 py-6 md:py-0 md:px-12 max-w-[800px]">
              <h2 class="text-5xl md:text-6xl xl:text-7xl font-bold tracking-tight leading-tight mb-12">
                The Batman
              </h2>
              <p class="text-lg">
                On Halloween, Gotham City mayor Don Mitchell Jr. is murdered by
                a masked psychopath calling himself the Riddler.
              </p>
            </div>
          </div>
        </div>
      </div>
    </router-link>
    <form @submit.prevent="searchMovies()">
      <label for="default-search" class="mb-2 text-sm font-medium text-gray-900 sr-only">Search</label>
      <div class="relative">
        <div class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none">
          <svg class="w-5 h-5 text-gray-500 " fill="none" stroke="currentColor" viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
          </svg>
        </div>
        <input type="search" id="default-search"
          class="block p-4 pl-10 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300"
          placeholder="What are you looking for?" v-model="search" required>
        <button type="submit"
          class="text-white absolute right-2.5 bottom-2.5 bg-green-400 font-medium rounded-lg text-sm px-4 py-2">Search</button>
      </div>
    </form>
    <div class="p-2 grid grid-cols-2 gap-3 lg:grid-cols-5 lg:gap-5">
      <div v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID">
          <div class="flex justify-center min-h-[750px]">
            <div class="rounded-lg shadow-lg bg-white max-w-sm">
              <img class="w-full rounded-t-lg h-[555px]" :src="movie.Poster" alt="Movie Poster" />
              <div class="p-6 text-center">
                <h5 class="text-gray-900 text-xl font-medium mb-2">{{ movie.Title }}</h5>
                <p class="text-gray-700 text-base mb-4 capitalize ">
                  {{ movie.Type }}
                </p>
                <p class="text-gray-700 text-base mb-4">
                  {{ movie.Year }}
                </p>
              </div>
            </div>
          </div>
        </router-link>
      </div>
    </div>

  </section>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js';

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const searchMovies = () => {
      if (search.value != "") {
        fetch(`${env.baseURL}/?apikey=${env.apikey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            console.log(data);
            movies.value = data.Search;
            search.value = "";
          });
      }
    }
    return {
      search,
      movies,
      searchMovies
    }
  }

}
</script>