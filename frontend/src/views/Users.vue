<template>
  <h1>Users</h1>
  <UsersTable v-if="users.length" :users="users" />
  <div v-if="usersLoadingError">{{ usersLoadingError }}</div>
</template>

<script>
// @ is an alias to /src
import UsersTable from "@/components/UsersTable.vue";
import axios from "axios";

export default {
  name: "Users",
  components: {
    UsersTable,
  },
  data: function () {
    return {
      users: [],
      usersLoadingError: "",
    };
  },
  methods: {
    fetchUsers: function () {
      axios
        .get(`${process.env.VUE_APP_BACKEND_BASE_URL}/users`)
        .then((response) => {
          this.users = response.data.users;
        })
        .catch((error) => {
          this.usersLoadingError = "An error occured while fetching users.";
          console.error(error);
        });
    },
  },
  mounted: function () {
    this.fetchUsers();
  },
};
</script>
