<script setup>

import {reactive, ref} from "vue";

let props =  defineProps({
  items: {
    type: Object,
    required: true,
  },
  actions: {
    type: Object,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  taskComponent: {
    type: Object,
    required: true,
  },
  formAddTaskComponent: {
    type: Object,
    required: true,
  },
});

let displayAll = ref({
  value: false,
  textAll: 'Afficher toutes les tâches',
  textDone: 'Afficher les tâches terminées',
});
</script>

<template>
    <h1>{{props.title}}</h1>
    <button @click="() => {displayAll.value = !displayAll.value}">{{displayAll.value? displayAll.textAll : displayAll.textDone}}</button>
    <component :is="props.formAddTaskComponent" :onAdd="props.actions.add" />

    <template v-for="item of props.items" :key="item.id">
      <component :is="props.taskComponent" :item="item" :actions="{onDelete: props.actions.delete, onEdit: props.actions.edit}"
                v-if="displayAll.value && !item.done || !displayAll.value" />
    </template>

</template>

