<script setup>
import { ref, onMounted } from 'vue';

const name = ref('John Doe');
const status = ref('active');
const tasks = ref(['Task 1', 'Task 2', 'Task 3']);
const newTask = ref('');

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending';
  } else if (status.value === 'pending') {
    status.value = 'inactive';
  } else {
    status.value = 'active';
  }
};

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    if (data) {
      tasks.value = data.map((task) => task.title);
    }
  } catch (error) {
    console.error('Error loading tasks:', error);
  }
});
const addTask = () => {
  if (newTask.value !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';
  };
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
}

</script>

<template>
  <h1>{{ name }}</h1>
  <br>
  <p v-if="status === 'active'">Status: Active</p>
  <p v-else-if="status === 'pending'">Status: Pending</p>
  <p v-else>Status: Inactive</p>
  <br>
  <!--
    @submit.prevent is a Vue.js directive that listens 
    for the submit event on a form and prevents the default browser 
    behavior of submitting the form and reloading the page. 
    This allows you to handle the form submission with JavaScript, 
    typically by calling a method defined in your Vue component, 
    without causing a page refresh.
  -->
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask">
    <button type="submit">Submit</button>
  </form>
  <h3>Tasks</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>
  <br>
  <!-- <button v-on:click="toggleStatus">Toggle Status</button> -->
  <button @click="toggleStatus">Toggle Status</button>
</template>
