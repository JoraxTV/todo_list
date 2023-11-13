<script setup lang="ts">
  import { ref, computed } from 'vue';
  import type { Ref } from 'vue';


  interface Tache {
    id: number;
    description: string;
    faite: boolean;
  }

  
  let id = 0;
  const taches:Ref<Tache[]> = ref([{ id: id++, description: "Apprendre Vue", faite: false },
  { id: id++, description: "Finir la SAÉ", faite: false },
  { id: id++, description: "Réviser pour l'interro", faite: false }]);


  let description = "";
  function ajouterTache(description: string) {
    if (description == "") return;
    taches.value.push({ id: id++, description: description, faite: false });
  }


  function retirerTache(id: number) {
    taches.value = taches.value.filter(tache => tache.id != id);
  }


  const cacheFaits = ref(false);
  const tachesFiltrees = computed(() => {
    return cacheFaits.value ? taches.value.filter(tache => !tache.faite) : taches.value;
  });
</script>

<template>
  <input type="text" v-model.trim="description" placeholder="Ajouter une tâche" /> <button
    @click="ajouterTache(description)">Ajouter</button>

  <div id="wrapper">
    <ul>
      <li v-for="tache in tachesFiltrees" :key="tache.id">
        <input type="checkbox" v-model="tache.faite" />
        <span class="description" :class="{fait:tache.faite, pasfait:!tache.faite}">{{tache.description}}</span>
        <button @click="retirerTache(tache.id)">Retirer</button>
      </li>
    </ul>
  </div>
  <button @click="cacheFaits = !cacheFaits">
    {{ cacheFaits ? 'Tout montrer' : 'Cacher les tâches terminées' }}
  </button>
</template>

<style scoped>
  #wrapper {
    border-radius: 5px;
    border: solid grey 2px;
    padding: 10px;
  }

  ul,
  span {
    padding: 10px;
  }

  li {
    list-style: none;
    padding: 2px 0px;
  }

  .fait {
    text-decoration: line-through;
    color: grey;
  }

  .pasfait {
    color: white;
  }
</style>