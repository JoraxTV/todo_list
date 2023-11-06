<script setup lang="ts">
import { ref } from "vue";
let url = "https://vuejs.org/";
let compteur = ref(0);
function incremente() {
  compteur.value++;
  console.log(compteur.value);
}
function onInput(event : any) {
  compteur.value = event.target.value;
}
</script>

<template>
  <h1><a v-bind:href="url">Site de Vue</a></h1>
  <button v-on:click="incremente">{{ compteur }}</button>
  <input type="number" v-on:input="onInput" v-bind="compteur" />
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>