<script setup lang="ts">
 import {ref} from 'vue';
  let id = 0;
  const taches = ref([{id:id++, description:"Apprendre Vue", faite:false},
    {id:id++, description:"Finir la SAÉ", faite:false},
    {id:id++, description:"Réviser pour l'interro", faite:false}]);
</script>

<template>
 <div id="wrapper">
    <ul>
      <li v-for="tache in taches" :key="tache.id">
   	 <span>{{tache.description}}</span>
      </li>
    </ul>
  </div>
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