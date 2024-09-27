<template>
  <h1>Bonjour {{ firstname }} <span v-html="lastname"></span></h1>

  <!-- Vuejs vas deconstruire l'objet c'est pour ca qu'on ne met pas count.value -->

  <!-- : indique c'est dynamique -->

  <!-- id dynamique -->
  <p :id="`p-${count}`">Counter : {{ count }}</p>

  <!-- style dynamique -->
  <p :style="{color: count >= 5 ? 'red' : 'green'}">Counter : {{ count }}</p>

  <!-- class dynamique -->
  <p :class="{active: count >= 5}">Counter : {{ count }}</p>

  <!-- 
  v-show -> afficher masquer un element
  v-if -> supprimer l'element du DOM
  v-hide -> l'inverse du show
   -->

  <div v-if="count >= 5">Bravo vous avez cliquer 5 fois</div>
  <div v-else>Vous avez cliquer moins de 5 fois</div>
  <button v-on:click="increment">Increment</button>
  <button @click="increment">Increment2</button>
  <button @click="decrement">Decrement</button>
  <p>Comment allez vous ?</p>
</template>

<script setup>
  import {
    ref
  } from 'vue';

  const firstname = "Dylane";
  const lastname = '<span>Tano</span>'
  let count = ref(0);
  const movies = ref([
    "Matrix",
    "Jujustu Kaisen",
    "Demon Slayer",
  ])

  // setInterval(() => {
  //   count.value++;
  // }, 1000);

  function increment(e) {
    console.log(e);
    count.value++;
  }
  const decrement = () => {
    count.value--;
  }
</script>

<style> 
.active {
  font-weight: bold;
  font-family: 'Lucida Sans', sans-serif;
}
</style>