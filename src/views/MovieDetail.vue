<template>
  <router-link to="/">
  <div class="back">
    <i class="fas fa-arrow-left"></i>
    back
  </div>
  </router-link>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
    <p class="year">{{ movie.Year }}</p>
    <p>{{ movie.Country }}, {{ movie.Runtime }}</p>
    <p>{{ movie.Rating }}</p>
    <p>{{ movie.Genre }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="feature-img" />
    <p class="plot">{{ movie.Plot }}</p>
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
  setup () {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
          // console.log(data);
          movie.value = data;
        });
    });

    return {
      movie
    }
  }
}
</script>

<style lang="scss">
.back {
  color: #06AD0C;
  font-size: 20px;
  margin-left: 5px;
  margin-top: 5px;
}

.movie-detail {
  padding: 16px;

  h2 {
    color: #fff;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }

  .feature-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }

  p {
    color: #E50914;
    font-size: 18px;
    line-height: 1.4;
    margin-bottom: 5px;
  }

  .year {
    color: #AAA;
  }

  .plot {
    color: #fff;
  }
}
</style>