<script async setup>
import Task from "./components/Task.vue";
import List from "./components/List.vue";
import {onMounted, reactive, ref} from "vue";
import FormAddTask from "@/components/FormAddTask.vue";
const getTasks = async () => {
  const res = await fetch("http://localhost:3000/tasks");
  return await res.json();
} ;
const editTask = async (task) => {

  const res = await fetch(`http://localhost:3000/tasks/${task.id}`, {
    method: 'PATCH',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(task)
  });
  const index = tasks.value.findIndex((t) => t.id === task.id);
  tasks.value[index] = await res.json();
};
const editStateTask = async (task) => {
  const res = await fetch(`http://localhost:3000/tasks/${task.id}`, {
    method: 'PATCH',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({done: !task.done})
  });
  const index = tasks.value.findIndex((t) => t.id === task.id);
  tasks.value[index] = await res.json();
};
const deleteTask = (task) => {
  fetch(`http://localhost:3000/tasks/${task.id}`, {
    method: 'DELETE',
  });
  const index = tasks.value.findIndex((t) => t.id === task.id);
  tasks.value.splice(index, 1);
};
const addTask = async (task) => {
  const res = await fetch(`http://localhost:3000/tasks`, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(task)
  });
  tasks.value.push(await res.json());
};
const tasks = ref([] );

onMounted(async () => {
  tasks.value = reactive(await getTasks());
});

</script>

<template>

  <List :task-component="Task"
        :form-add-task-component="FormAddTask"
        :items="tasks" :title="'Todo List - ESGI Vue projct'"
        :actions="{edit: editTask, delete: deleteTask, add: addTask, onStateEdit: editStateTask}" />

</template>

<style>

* {
  box-sizing: border-box;
}

html,body {
  margin: 0;
  padding: 0;
  font-family: 'Roboto', sans-serif;
}

html {
  background: darkorange;
  color : white;
  text-align: center;
}

h1 {
  margin: 0 ;
  margin-top: 50px ;
}

</style>