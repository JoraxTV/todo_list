<script setup lang="ts">
 import {ref} from 'vue';
  let id = 0;
  const taches = ref([{id:id++, description:"Apprendre Vue", faite:false},
    {id:id++, description:"Finir la SAÉ", faite:false},
    {id:id++, description:"Réviser pour l'interro", faite:false}]);
  
  let description = "";
  function ajouterTache(description:string){
    if (description == "") return;
    taches.value.push({id:id++, description:description, faite:false});
  }

  function retirerTache(id:number){
    taches.value = taches.value.filter(tache => tache.id != id);
  }

  const cacheFaits = ref(false);

  function tachesFiltrees(){
    return cacheFaits.value ? taches.value.filter(tache => !tache.faite) : taches.value;
  }
</script>

<template>
  <button @click="cacheFaits = !cacheFaits">
    {{ cacheFaits ? 'Tout montrer' : 'Cacher les tâches terminées' }}
</button>
  <input type="text" v-model.trim="description" placeholder="Ajouter une tâche"/>
  <button @click="ajouterTache(description)">Ajouter</button>
  <div id="wrapper">
      <ul>
        <li v-for="tache in tachesFiltrees()" :key="tache.id">
          <input type="checkbox" v-model="tache.faite"/>
          <span class="description" :class="{fait:tache.faite, pasfait:!tache.faite}">{{tache.description}}</span>
          <button @click="retirerTache(tache.id)">Retirer</button>
        </li>
      </ul>
    </div>
</template>

<style scoped>
body{
  font-family: sans-serif;
  font-size: 1.2rem;
  line-height: 1.5;
  color: #333;
  margin: 0;
  padding: 0;
}

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
#wrapper{
   border-radius: 5px;
   border:solid black 2px;
   padding: 10px;
 }
 ul,span{
   padding:10px;
 }
 li{
   list-style: none;
   padding: 2px 0px;
 }
 
 .fait{
   text-decoration: line-through;
   color: grey;
 }
 .pasfait{
   color: white;
 }
</style>