<template>
    <div class="container px-6 mx-auto mt-5">
        <section class="mb-32 text-gray-800">
            <div class="container mx-auto xl:px-32 text-center lg:text-left">
                <div class="grid lg:grid-cols-2 flex items-center">
                    <div class="mb-12 lg:mb-0">
                        <div class="block rounded-lg shadow-lg px-6 py-12 md:px-12 lg:-mr-14"
                            style="background: hsla(0, 0%, 100%, 0.55); backdrop-filter: blur(30px)">
                            <h2 class="text-3xl font-bold mb-6">{{ movie.Title }}</h2>
                            <p class="text-gray-500 mb-6 pb-2 lg:pb-0">
                                {{ movie.Plot }}
                            </p>
                            <div class="flex flex-col md:flex-row md:justify-around lg:justify-between mb-6 mx-auto">
                                <p class="flex items-center mb-4 md:mb-2 lg:mb-0 mx-auto md:mx-0">
                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="w-4 h-4 mr-2">
                                        <path fill="currentColor"
                                            d="M504 256c0 136.967-111.033 248-248 248S8 392.967 8 256 119.033 8 256 8s248 111.033 248 248zM227.314 387.314l184-184c6.248-6.248 6.248-16.379 0-22.627l-22.627-22.627c-6.248-6.249-16.379-6.249-22.628 0L216 308.118l-70.059-70.059c-6.248-6.248-16.379-6.248-22.628 0l-22.627 22.627c-6.248 6.248-6.248 16.379 0 22.627l104 104c6.249 6.249 16.379 6.249 22.628.001z">
                                        </path>
                                    </svg>
                                    Rated {{ movie.Rated }}
                                </p>
                                <p class="flex items-center mb-4 md:mb-2 lg:mb-0 mx-auto md:mx-0">
                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="w-4 h-4 mr-2">
                                        <path fill="currentColor"
                                            d="M504 256c0 136.967-111.033 248-248 248S8 392.967 8 256 119.033 8 256 8s248 111.033 248 248zM227.314 387.314l184-184c6.248-6.248 6.248-16.379 0-22.627l-22.627-22.627c-6.248-6.249-16.379-6.249-22.628 0L216 308.118l-70.059-70.059c-6.248-6.248-16.379-6.248-22.628 0l-22.627 22.627c-6.248 6.248-6.248 16.379 0 22.627l104 104c6.249 6.249 16.379 6.249 22.628.001z">
                                        </path>
                                    </svg>
                                    Metascore {{ movie.Metascore }}
                                </p>
                                <p class="flex items-center mb-2 lg:mb-0 mx-auto md:mx-0">
                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="w-4 h-4 mr-2">
                                        <path fill="currentColor"
                                            d="M504 256c0 136.967-111.033 248-248 248S8 392.967 8 256 119.033 8 256 8s248 111.033 248 248zM227.314 387.314l184-184c6.248-6.248 6.248-16.379 0-22.627l-22.627-22.627c-6.248-6.249-16.379-6.249-22.628 0L216 308.118l-70.059-70.059c-6.248-6.248-16.379-6.248-22.628 0l-22.627 22.627c-6.248 6.248-6.248 16.379 0 22.627l104 104c6.249 6.249 16.379 6.249 22.628.001z">
                                        </path>
                                    </svg>
                                    IMDB Score {{ movie.Rating }}
                                </p>
                            </div>
                        </div>
                    </div>
                    <div>
                        <img :src="movie.Poster" class="w-full rounded-lg shadow-lg h-[500px] lg:h-[700px]" alt="" />
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
    setup() {
        const movie = ref({});
        const route = useRoute();

        onBeforeMount(() => {
            fetch(`${env.baseURL}/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
                .then(response => response.json())
                .then(data => {
                    console.log(data);
                    movie.value = data;
                });
        });

        return {
            movie,
            route
        }
    }
}
</script>