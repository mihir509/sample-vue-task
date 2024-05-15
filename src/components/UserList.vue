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
    ...mapState(['currentPage', 'searchFilter', 'users']), // Map 'users' state
    ...mapGetters(['paginatedUsers']),
    filteredPaginatedUsers() {
      if (!this.searchFilter || !this.searchFilter.searchTerm) {
        return this.paginatedUsers;
      }

      const searchTerm = this.searchFilter.searchTerm.toLowerCase();
      const filter = this.searchFilter.selectedFilter;

      let filteredData = this.paginatedUsers;

      if (filter === 'All') {
        filteredData = this.users; // Use 'users' state
      }

      if (!Array.isArray(filteredData)) {
        return [];
      }

      filteredData = filteredData.filter(user => {
        if (filter === 'All') {
          return (
            user.name.toLowerCase().includes(searchTerm) ||
            user.email.toLowerCase().includes(searchTerm) ||
            user.phone.toLowerCase().includes(searchTerm) ||
            user.website.toLowerCase().includes(searchTerm) ||
            user.company.name.toLowerCase().includes(searchTerm)
          );
        } else if (filter === 'User') {
          return user.name.toLowerCase().includes(searchTerm) || user.email.toLowerCase().includes(searchTerm);
        } else if (filter === 'Phone') {
          return user.phone.toLowerCase().includes(searchTerm);
        }
      });

      return filteredData.slice(0, this.usersPerPage);
    }
  }
}
</script>
