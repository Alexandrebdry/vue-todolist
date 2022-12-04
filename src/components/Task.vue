<script setup>
import {ref} from "vue";

const props = defineProps({
  item: {
    type: Object,
    required: true,
  },
  actions: {
    type: Object,
    required: true,
  },
});
const task = ref(props.item);

</script>

<template>
  <div :style="{display:'flex', alignItems:'center', justifyContent:'center', flexDirection:'column'}">
    <div :style="{display:'flex', alignItems:'center', justifyContent:'center'}">
      <p>{{task.title}}</p>
      <span>{{task.done ? '✅' : '❌' }}</span>
    </div>
    <button @click="props.actions.onEdit({...task, done: !task.done})">{{task.done ? 'set to todo' : 'set to done'}}</button>
    <div>
      <form @submit.prevent="props.actions.onEdit(task)">
        <input type="text" v-model="task.title">
        <button type="submit">edit</button>
      </form>
    </div>
    <button @click="props.actions.onDelete(task)">Delete</button>

  </div>

</template>