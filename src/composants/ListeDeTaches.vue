<script setup lang="ts">
import { ref, computed, defineEmits } from 'vue';
import type { Ref } from 'vue';
import TacheElement from '@/composants/TacheElement.vue';

interface Tache {
  id: number;
  description: string;
  faite: boolean;
}

const props = defineProps({
  titre: String,
});

const emit = defineEmits<{
  supprimerTache: [],
  checkedChange: [boolean];
}>();

let id = 0;
const taches: Ref<Tache[]> = ref([
  { id: id++, description: "Apprendre Vue", faite: false },
  { id: id++, description: "Finir la SAÉ", faite: false },
  { id: id++, description: "Réviser pour l'interro", faite: false },
]);

const description = ref("");
const ajouterTache = (description: string) => {
  if (description === "") return;
  taches.value.push({ id: id++, description: description, faite: false });
};

const retirerTache = (id: number) => {
  taches.value = taches.value.filter(tache => tache.id !== id);
};

const supprimerListe = () => {
  emit('supprimerTache');
};

const cacheFaits = ref(false);
const tachesFiltrees = computed(() => {
  return cacheFaits.value ? taches.value.filter(tache => !tache.faite) : taches.value;
});
</script>

<template>
  <div id="wrapper">
    <h2>{{ titre }}</h2>
    <input type="text" v-model.trim="description" placeholder="Ajouter une tâche" /> <button
    @click="ajouterTache(description)">Ajouter</button>
    <ul>
      <li v-for="tache in tachesFiltrees" :key="tache.id">
        <TacheElement
        :description-tache="tache.description"
        v-model="tache.faite"
        @supprimer-tache="retirerTache(tache.id)"
        />
      </li>
    </ul>
    <button @click="cacheFaits = !cacheFaits">
      {{ cacheFaits ? 'Tout montrer' : 'Cacher les tâches terminées' }}
    </button>
  </div>
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

  h2 {
        color: #afbedd;
    }

    button {
        background-color: #afbedd;
        border: none;
        color: white;
        padding: 5px 10px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 12px;
        border-radius: 5px;
    }

    button:hover {
        background-color: #8f9ec5;
    }
</style>