<template>
     <div>
    <input type="text" class="form-control" v-model="searchFilter" @input="updateFilter" placeholder="Search..." />
  </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        searchFilter: ''
      }
    },
    methods: {
      updateFilter() {
        this.$emit('filterChanged', this.searchFilter);
      }
    }
  }
  </script>