<script>

  export default {
    name: 'App',
    data() {
      return {
        name: 'John Doe',
        status: 'pending',
        tasks: ['Task One', 'Task Two', 'Task Three'],
        link: 'https://www.google.com'
      }
    },
    created() {
      fetch('https://jobs.github.com/positions.json')
        .then(response => response.json())
        .then(data => {
          this.jobs = data
        })
    }
  }
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">Status: Active</p>
  <p v-else-if="status === 'pending'">Status: Pending</p>
  <p v-else>Status: Inactive</p>

  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li> 
    <a v-bind:href="link">Google</a>
  </ul>
</template>

