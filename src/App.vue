<script setup>
import { ref } from 'vue';

const name = ref('John Doe');
const status = ref('active');
const tasks = ref(['Task 1', 'Task 2', 'Task 3']);

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending';
  } else if (status.value === 'pending') {
    status.value = 'inactive';
  } else {
    status.value = 'active';
  }
};

</script>

<template>
  <h1>{{ name }}</h1>
  <br>
  <p v-if="status === 'active'">Status: Active</p>
  <p v-else-if="status === 'pending'">Status: Pending</p>
  <p v-else>Status: Inactive</p>
  <br>
  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <br>
  <!-- <button v-on:click="toggleStatus">Toggle Status</button> -->
  <button @click="toggleStatus">Toggle Status</button>
</template>
