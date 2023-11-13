<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';

const props = defineProps<{ modelValue: boolean }>();

const emit = defineEmits(['update:modelValue', 'supprimerTache']);
</script>

<template>
  <div>
    <input type="checkbox" :checked="props.modelValue" @change="$emit('update:modelValue', ($event.target as HTMLInputElement).checked)" />
    <span :class="{ fait: props.modelValue, pasfait: !props.modelValue }"><slot></slot></span>
    <button @click="$emit('supprimerTache')">Retirer</button>
  </div>
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