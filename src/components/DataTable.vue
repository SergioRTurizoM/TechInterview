<template>
  <v-row justify="center">
    <v-col cols="12">
      <v-card>
        <v-card-title>Data Table</v-card-title>
        <v-card-subtitle>
          <p>Users data</p>
        </v-card-subtitle>
        <SearchTable @search="handleSearch" />
        <v-data-table
          :headers="headers"
          :items="filteredUsers"
          :footer-props="{ 'items-per-page-options': [10, 20, 30] }"
          :options="{ itemsPerPage: pagination.rowsPerPage }"
          dense
          transition= "scale-transition"
        >
          <template slot="items" slot-scope="props">
            <td>{{ props.item.id }}</td>
            <td>{{ props.item.first_name }}</td>
            <td>{{ props.item.username }}</td>
            <td>{{ props.item.employment.title }}</td>
            <td>{{ props.item.subscription.status }}</td>
            <td>{{ props.item.email }}</td>
            <td>{{ props.item.address.city }}</td>
          </template>
        </v-data-table>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import axios from "axios";
import SearchTable from "../components/SearchTable.vue";

export default {
  components: { SearchTable },
  data() {
    return {
      headers: [
        { text: "Id", value: "id" },
        { text: "First Name", value: "first_name" },
        { text: "Username", value: "username" },
        { text: "Title", value: "employment.title" },
        { text: "Subscription", value: "subscription.status" },
        { text: "Email", value: "email" },
        { text: "City", value: "address.city" },
      ],
      users: [],
      search: "",
      pagination: {
        rowsPerPage: 10,
      },
    };
  },
  computed: {
    filteredUsers() {
      return this.users.filter(
        (user) =>
          user.first_name.toLowerCase().includes(this.search.toLowerCase()) ||
          user.id.toString().includes(this.search) ||
          user.username.toLowerCase().includes(this.search.toLowerCase()) ||
          user.employment.title
            .toLowerCase()
            .includes(this.search.toLowerCase()) ||
          user.subscription.status
            .toLowerCase()
            .includes(this.search.toLowerCase()) ||
          user.email.toLowerCase().includes(this.search.toLowerCase()) ||
          user.address.city.toLowerCase().includes(this.search.toLowerCase())
      );
    },
  },
  created() {
    this.fetchUsers();
  },
  methods: {
    fetchUsers() {
      const url_base_users= "https://random-data-api.com/api/users/random_user"
      axios
        .get(`${url_base_users}?size=50`)
        .then((response) => {
          this.users = response.data;
        })
        .catch((error) => {
          console.error("There was an error!", error);
        });
    },
    handleSearch(search) {
      this.search = search;
    },
  },
};
</script>

