<script setup>
import { ref } from "vue";
import axios from "axios";
 
const movies = ref ("");
const response = ref(null);

const getMovies = async () => {
    console.log(movies.value)
    response.value = (await getData(`https://api.themoviedb.org/3/trending/movie/week`, {
    params: {
      api_key: "5ee6242bedc5de8c07acae66ee444042",
    }
  })).data ['results'];
}
 
const getData = async (url, params) => {
try {
  return await axios.get(url, params);
} catch (error) {
  console.log(error);
}
};
 
</script>

<template>
   <div v-if="getMovies()" v-for="result in response" class="column" >
      <!--<p>{{result.original_title}}</p>-->
      <img v-bind:src="'http://image.tmdb.org/t/p/w500/' + result.poster_path">
    </div>
</template>

<style scoped>


</style>