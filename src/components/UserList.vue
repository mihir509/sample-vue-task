<template>
    <div>
      <table class="table">
      <thead>
        <tr>
          <th>No</th>
          <th>Name</th>
          <th>Email</th>
          <th>Phone</th>
          <th>Website</th>
          <th>Company Name</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in filteredPaginatedUsers" :key="user.id">
          <td>{{ user.id }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.phone }}</td>
          <td>{{ user.website }}</td>
          <td>{{ user.company.name }}</td>
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
        || user.phone.toLowerCase().includes(this.searchFilter.toLowerCase()) 
        || user.website.toLowerCase().includes(this.searchFilter.toLowerCase())
        || user.company.name.toLowerCase().includes(this.searchFilter.toLowerCase())
      );
    }
  }
}
</script>
