<template>
  <h1>Bonjour {{ firstname }}</h1>
  <p>Counter : {{ count }}</p>
  <button>Increment</button>
  <button @click="increment">Increment2</button>
  <button @click="decrement">Decrement</button>
  <p>Comment allez vous ?</p>
</template>

<script setup>
import { ref } from 'vue';
const firstname = "Dylane";

let count = ref(0);

// setInterval(() => {
//   count.value++;
// }, 1000);

function increment(){
  count.value++;
}

const decrement = () => {
  count.value--;
}
</script>