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
          :items="tasks" :title="'List'"
          :actions="{edit: editTask, delete: deleteTask, add: addTask}" />
</template>