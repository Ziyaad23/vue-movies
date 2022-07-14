<template>
    <div>
        <h2>{{ movie.Title }}</h2>
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