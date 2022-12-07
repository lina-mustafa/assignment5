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
   <div v-if="getMovies()" v-for="result in response" class="grid-container">
      <!--<p>{{result.original_title}}</p>-->
      <img v-bind:src="'http://image.tmdb.org/t/p/w500/' + result.poster_path">
    </div>
</template>

<style scoped>
.grid-container {
  display: grid;
  grid-template-rows: auto auto auto;
  padding: 10px;
}
.grid-item {
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  padding: 20px;
  font-size: 30px;
  text-align: center;
}
</style>