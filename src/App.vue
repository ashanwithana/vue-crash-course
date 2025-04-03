<script setup>
import { onMounted, ref } from 'vue';

const message = ref('Hi There');
const status = ref('inactive');
const boys = ref(['ashan', 'nishen', 'dushen']);
const link = ref('https://www.google.com');
const tasks = ref(['task 1', 'task 2', 'task 3']);
const newTask = ref('');

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending'
  } else if (status.value === 'pending') {
    status.value = 'inactive'
  } else {
    status.value = 'active'
  }
}

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
  }
}
const deleteTask = (index) => {
  tasks.value.splice(index, 1);
}

onMounted(async()=>{
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/todos');
  const data = await res.json();
  tasks.value = data.map((task)=> task.title);
  } catch (error) {
    console.error('Error fetching data:', error);
  }
})

</script>

<template>
  <h1>{{ message }}</h1>
  <p v-if="status === 'active'">User is Activated</p>
  <p v-else-if="status === 'pending'">User is Pending</p>
  <p v-else>User is Inactive</p>

  <h2>Boys List</h2>
  <ul>
    <li v-for="boy in boys" :key="boy">{{ boy }}</li>
  </ul>
  <!-- <a v-bind:href="link">Click for Google Search</a> -->
  <a :href="link">Click for Google Search</a>
  <br>
  <button v-on:click="toggleStatus">Change Status</button>
  <br><br>

  <form @submit.prevent="addTask">
    <label for="task">Add New Task</label>
    <input type="text" name="newTask" id="newTask" v-model="newTask" />
    <button type="submit">Add Task</button>
  </form>

  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>
</template>
