<script setup>
import { ref } from "vue";
import axios from "axios";

const props = defineProps(["id"]);
const response = ref(null);
const emits = defineEmits(["toggleModal"]);
 
const getData = async (url, params) => {
try {
  return await axios.get(url, params);
} catch (error) {
  console.log(error);
}
};
 
const getMovies = async (movies) => {
  response.value = (await getData(`https://api.themoviedb.org/3/movie/${movies}`, {
    params: {
      api_key: "5ee6242bedc5de8c07acae66ee444042",
    }
  })).data;
}
</script>

<template>
  <Teleport to="body">
    <div v-if= "getMovies(props.id)" class="modal-outer-container" @click.self="emits('toggleModal')">
      <div class="modal-inner-container">
        <button class="close-button" @click="emits('toggleModal')">X</button>
        <p>{{response.title}}</p>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
.modal-outer-container {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background: #00000099;
  z-index: 3;
}

.modal-outer-container .modal-inner-container {
  background-color: #1F2123;
  color: white;
  width: clamp(280px, 100%, 800px);
  height: 400px;
  position: relative;
}

.modal-outer-container .modal-inner-container .close-button {
  position: absolute;
  right: 0px;
  padding: 1rem;
  border: none;
  background: #1F2123;
  font-weight: bold;
  font-size: 1.25rem;
  color: white;
}
</style>
