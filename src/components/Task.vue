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
  <div :style="{display:'flex', alignItems:'center', justifyContent:'center', flexDirection:'column', paddingBottom: '5px'}">
    <div :style="{display:'flex', alignItems:'center', justifyContent:'center'}">
      <form @submit.prevent="props.actions.onEdit({...task, done: props.item.done})">
        <input type="text" v-model="task.title">
        <span :class="'btn'" @click="props.actions.onEdit({...props.item, done: !props.item.done})">{{props.item.done ? '✅' : '❌' }}</span>
        <button type="submit">edit</button>
      </form>
      <button @click="props.actions.onDelete(props.item)">Delete</button>
    </div>

  </div>

</template>

<style scoped>
.btn {
    margin: 0 5px;
    cursor: pointer;
  }

form {
  display: flex;
  align-items: center;
  justify-content: center;

}
form > input {
  width: 24.5vw;
}
</style>