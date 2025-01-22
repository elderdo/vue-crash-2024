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
  methods: {
    toggleStatus() {
      if (this.status === 'active') {
        this.status = 'pending'
      } else if (this.status === 'pending') {
        this.status = 'inactive'
      } else {
        this.status = 'active'
      }
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
  <br>
  <p v-if="status === 'active'">Status: Active</p>
  <p v-else-if="status === 'pending'">Status: Pending</p>
  <p v-else>Status: Inactive</p>
  <br>
  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <!-- <a v-bind:href="link">Google</a> -->
  <a :href="link">Google</a>
  <br>
  <!-- <button v-on:click="toggleStatus">Toggle Status</button> -->
  <button @click="toggleStatus">Toggle Status</button>
</template>
