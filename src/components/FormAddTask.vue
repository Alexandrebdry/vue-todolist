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

  <p>Ajouter une nouvelle tâche</p>
  <form @submit.prevent="handleSubmit(task)">
    <input type="text" v-model="task.title" />
    <button type="submit">Add</button>
  </form>


</template>

<style scoped>
p {
  margin: 0;
  margin-top: 15px
}
form {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 55px;
}
form > input {
  width: 30vw;
}
</style>

