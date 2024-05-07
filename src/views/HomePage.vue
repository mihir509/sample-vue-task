<template>
    <div id="app">
        <div class="container">
            <div class="d-flex justify-content-between align-items-center">
            <SearchFilter @filterChanged="updateFilter" />
            <RouterLink to="/form"><button class="btn-primary">Add User</button></RouterLink>
            </div>
            <div class="my-3">  
            <UserList :users="filteredUsers" />
           
            </div>
            <div class="d-flex justify-content-end align-items-center">
            <UserPagination :currentPage="currentPage" :totalPages="totalPages" @pageChanged="updatePage" />
            </div>
        </div>
    </div>
</template>

<script>
import { mapState } from 'vuex';
import SearchFilter from '@/components/SearchFilter.vue';
import UserList from '@/components/UserList.vue';
import UserPagination from '@/components/UserPagination.vue'
export default {
    name:'HomePage',
    components: {
        SearchFilter,
        UserList,
        UserPagination
    },
    computed: {
        ...mapState(['users', 'currentPage', 'totalPages', 'searchFilter']),
        filteredUsers() {
            return this.users.filter(user =>
                user.name.toLowerCase().includes(this.searchFilter.toLowerCase())
                || user.email.toLowerCase().includes(this.searchFilter.toLowerCase())
            );
        }
    },
    methods: {
        updatePage(page) {
            this.$store.dispatch('updatePage', page);
        },
        updateFilter(filter) {
            this.$store.dispatch('updateFilter', filter);
        }
    },
    created() {
        this.$store.dispatch('fetchUsers');
    }
}
</script>