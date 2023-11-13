<script setup lang="ts">
import ListeDeTaches from '@/composants/ListeDeTaches.vue';
import { ref } from 'vue';

// Tableau réactif pour les listes de tâches
const todoListes = ref([
  { id: 1, titre: 'Liste 1', taches: [
    { id: 1, description: 'Tâche 1 Liste 1', faite: false },
    { id: 2, description: 'Tâche 2 Liste 1', faite: true },
    // ... autres tâches
  ] },
  { id: 2, titre: 'Liste 2', taches: [
    { id: 1, description: 'Tâche 1 Liste 2', faite: false },
    { id: 2, description: 'Tâche 2 Liste 2', faite: true },
    // ... autres tâches
  ] },
]);

// Variable pour stocker le titre de la nouvelle liste
const nouveauTitre = ref('');

// Fonction pour ajouter une nouvelle liste de tâches
const ajouterListe = () => {
  const nouvelleListe = {
    id: todoListes.value.length + 1,
    titre: nouveauTitre.value,
    taches: [], // Initialiser la liste de tâches vide
  };

  todoListes.value.push(nouvelleListe);
  nouveauTitre.value = ''; // Réinitialise le champ d'entrée
};

// Fonction pour supprimer une liste de tâches
const retirerListe = (id: number, titre: string) => {
  if (confirm(`Voulez-vous vraiment supprimer la liste "${titre}"?`)) {
    todoListes.value = todoListes.value.filter(liste => liste.id != id);
  }
};

</script>

<template>
  <div>
    <div v-for="liste in todoListes" :key="liste.id">
      <button class="supprimer" @click="retirerListe(liste.id, liste.titre)">x</button>
      <ListeDeTaches :tasks="liste.taches" :titre="liste.titre" />
    </div>

    <div>
      <input v-model="nouveauTitre" placeholder="Nouvelle Liste de Tâches" />
      <button @click="ajouterListe">Ajouter Liste</button>
    </div>
  </div>
</template>

<style scoped>
/* Vos styles CSS ici */
.supprimer {
  float: right;
  margin: 0.5em;
  padding: 0.5em;
  border-radius: 5px;
  background-color: red;
  color: white;
  border: none;
  font-weight: bold;
  cursor: pointer;
}
</style>
