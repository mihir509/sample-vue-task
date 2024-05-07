<template>
    <div>
      <table class="table">
      <thead>
        <tr>
          <th>Name</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in filteredPaginatedUsers" :key="user.id">
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
        </tr>
      </tbody>
    </table>
    </div>
  </template>
  
  <script>
import { mapState, mapGetters } from 'vuex';

export default {
  computed: {
    ...mapState(['currentPage', 'searchFilter']),
    ...mapGetters(['paginatedUsers']),
    filteredPaginatedUsers() {
      return this.paginatedUsers.filter(user => 
        user.name.toLowerCase().includes(this.searchFilter.toLowerCase())
        || user.email.toLowerCase().includes(this.searchFilter.toLowerCase())
      );
    }
  }
}
</script>
