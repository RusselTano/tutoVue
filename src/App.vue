<template>
  <h1>Bonjour {{ firstname }} <span v-html="lastname"></span></h1>

  <!-- Vuejs vas deconstruire l'objet c'est pour ca qu'on ne met pas count.value -->

  <!-- : indique c'est dynamique -->

  <!-- id dynamique -->
  <p :id="`p-${count}`">Counter : {{ count }}</p>

  <!-- style dynamique -->
  <p :style="{ color: count >= 5 ? 'red' : 'green' }">Counter : {{ count }}</p>

  <!-- class dynamique -->
  <p :class="{ active: count >= 5 }">Counter : {{ count }}</p>

  <!-- 
  v-show -> afficher masquer un element
  v-if -> supprimer l'element du DOM
  v-hide -> l'inverse du show
   -->

  <div v-if="count >= 5">Bravo vous avez cliquer 5 fois</div>
  <div v-else>Vous avez cliquer moins de 5 fois</div>
  <div class="buttons__container">
    <button v-on:click="increment">Increment</button>
    <button @click="increment">Increment2</button>
    <button @click="decrement">Decrement</button>
  </div>
  <p>Comment allez vous ?</p>
<div class="buttons__container">
  <button @click="movies.sort()">Reorganiser</button>
  <button @click="sortMovies">Reorganiser2</button>
</div>
<form action="" @submit.prevent="addMovie">
  <!-- v-model -> en live -->
  <!-- <input type="text" placeholder="New movie" v-model="movieName">{{ movieName }} -->
  <input type="text" placeholder="New movie" v-model="movieName">
  <button type="submit">Add movie</button>
</form>
  <ul>
    <li v-for="movie in movies" :key="movie">
      <span>{{ movie }}</span> <button class="delete-button" @click="deleteMovie(movie)">Supprimer</button>
    </li>
  </ul>

  <ul>
    <li>{{ person.firstName }}</li>
    <li>{{ person.lastName }}</li>
    <li>{{ person.age }}</li>
  </ul>
  <button @click.prevent="randomAge">edit age</button>
</template>

<script setup>
import { ref } from "vue";

const firstname = "Dylane";
const lastname = "<span>Tano</span>";
const movieName = ref('');
let count = ref(0);
const movies = ref(["Matrix", "Jujustu Kaisen", "Demon Slayer"]);

const person = ref({firstName: "Dylane", lastName: "Tano", age: 19, couple: false})

// setInterval(() => {
//   count.value++;
// }, 1000);

function increment(e) {
  console.log(e);
  count.value++;
}
const decrement = () => {
  count.value--;
};
const deleteMovie = (movie) => {
  movies.value = movies.value.filter((m) => m !== movie);
};
const sortMovies = () => {
  movies.value.sort((a,b) => a > b ? 1 : -1);
}
const addMovie = () => {
  movies.value.push(movieName.value);
  movieName.value = '';
}
// Avant on etait oblige de faire le destructuring Ex: ...person.value
// const randomAge = () => {
//   person.value = {
//     ...person.value,
//     age: Math.round(Math.random() * 100)
//   }
// }

// Mais grace a la ref on peut modifier directement l'age
const randomAge = () =>{
  person.value.age = Math.round(Math.random() * 100)
}
</script>

<style>
.active {
  font-weight: bold;
  font-family: "Lucida Sans", sans-serif;
}
.buttons__container{
  display: flex;
  gap: 20px;
}
button {
  cursor: pointer;
  padding: 10px 12px;
  background-color: green;
  color: #fff;
  outline: none;
  border: 0;
  border-radius: 5px;
  font-weight: bold;
  box-shadow: 0 2px 3px 2px rgba(0, 0, 0, 0.4);
  transition: .3s ease-out;
}
button:hover{
  scale: 1.05;
}
.delete-button {
  background-color: crimson;
}
ul {
  display: grid;
  gap: 10px;
}
li{
  display: flex;
  gap: 20px;
  background-color: rgba(0, 0, 0, 0.1);
  padding: 10px 15px;
  border-radius: 10px;
  align-items: center;
  justify-content: space-evenly;
  /* width: 50%; */
  /* background-color: red; */
}
li span {
  width: 50%;
}

form{
  margin-top: 10px;
  display: flex;
  justify-content: center;
  gap: 20px;
}
form input {
  padding: 10px 15px;
  outline: none;
  border-radius: 5px;
}
</style>
