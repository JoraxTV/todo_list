<script setup lang="ts">
  import {ref} from 'vue';

  const props = defineProps<{descriptionTache: string, cochee:boolean}>();
</script>

<template>
    <input type ="checkbox" :checked="props.cochee">
    <span :class="{fait:props.cochee, pasfait:!props.cochee}">{{props.descriptionTache}}</span>
    <button @click="$emit('supprimerTache')">Retirer</button>
</template>

<style scoped>
  .fait {
    text-decoration: line-through;
    color: grey;
  }

  .pasfait {
    color: white;
  }
</style>