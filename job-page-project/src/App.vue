<script setup>
  import { onMounted, ref } from 'vue';
  const name = ref('Bob');
  const status = ref('active');
  const tasks = ref(['task1', 'task2', 'task3']);
  const newTask = ref('');

  const toggleStatus = () => {
    if (status.value === 'active') {
      status.value = 'pending'
    } else {
      status.value = 'active'
    }
  }

  const addTask = () => {
    if (newTask.value.trim() !== '') {
      tasks.value.push(newTask.value);
      newTask.value = '';
    }
  }

  const deleteTask = (index) => {
    tasks.value.splice(index, 1);
  }

  onMounted(async () => {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/todos');
      const data = await response.json();
      tasks.value = data.map((task) => task.title);
    } catch (error) {
      console.log('Error fetching tasks');
    }
  });
</script>

<template>

  <h1>{{name}}</h1>

  <!-- v-if -->
  <p v-if="status === 'active'">User is active</p>

  <!-- v-if -->
  <p v-else-if="status === 'pending'">User is loading</p>

  <!-- v-if -->
  <p v-else>User is inactive</p>

  <!-- v-for -->
  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>

  <!-- v-bind -->
  <a v-bind:href="link">Click for google</a>
  <a :href="link">Click</a>

  <!-- v-on -->
  <button v-on:click="toggleStatus">Change status</button>
  <button @click="toggleStatus"> Change status</button>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask">
    <button type="submit">Submit</button>
  </form>
</template>

<style scoped>
  button {
    cursor: pointer;
  }
</style>
