<script>
import { ref } from 'vue';

// Longform
export default {
  setup() {
    const name = ref('Bob');
    const status = ref('active');
    const tasks = ref(['task1', 'task2', 'task3']);

    const toggleStatus = () => {
      if (status.value === 'active') {
        status.value = 'pending'
      } else {
        status.value = 'active'
      }
    }

    return {
      name, 
      status,
      tasks,
      toggleStatus
    }
  },
}
</script>

<!--Shortform-->
<script setup>
import { ref } from 'vue';
    const name = ref('Bob');
    const status = ref('active');
    const tasks = ref(['task1', 'task2', 'task3']);

    const toggleStatus = () => {
      if (status.value === 'active') {
        status.value = 'pending'
      } else {
        status.value = 'active'
      }
    }
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
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>

  <!-- v-bind -->
  <a v-bind:href="link">Click for google</a>
  <a :href="link">Click</a>

  <!-- v-on -->
  <button v-on:click="toggleStatus">Change status</button>
  <button @click="toggleStatus"> Change status</button>

</template>

<style scoped>
  button {
    cursor: pointer;
  }
</style>
