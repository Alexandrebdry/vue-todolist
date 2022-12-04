<script setup>
import {ref} from "vue";

const task = ref({
  title: '',
  done: false
});

const props = defineProps({
  onAdd: {
    type: Function,
    required: true,
  },
});
const handleSubmit = (e) => {
  if(task.value.title !== ''){
    props.onAdd(task.value);
    task.value.title = '';
  }

};
</script>

<template>

  <p>Ajouter des taches</p>
  <form @submit.prevent="handleSubmit(task)">
    <input type="text" v-model="task.title" />
    <input type="checkbox" v-model="task.done" />
    <button type="submit">Add</button>
  </form>


</template>

