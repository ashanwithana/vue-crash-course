<script>
export default {
  data() {
    return {
      message: 'Hello Vue 3!',
      status: 'pending',
      boys: ['ashan', 'nishen', 'dushen'],
      link: 'https://www.google.com',
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
    },
  },
}
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

  <button v-on:click="toggleStatus">Change Status</button>
</template>
