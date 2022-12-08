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
  <h1>Trending Movies:</h1>
   <div v-if="getMovies()" v-for="result in response" class="grid-container">
      <!--<p>{{result.original_title}}</p>-->
      <img v-bind:src="'http://image.tmdb.org/t/p/w500/' + result.poster_path">
    </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap");

.grid-container{
  display: flex;
  display: inline-grid;
  align-content: space-evenly;
  padding: 20px;
  gap: 10%;
  margin-bottom: -260px;
}

img{
  height:50%;
}

h1{
  font-family: 'Bebas Neue', cursive;
  font-size: 100px;
  color: rgb(229, 9, 20);
}


</style>