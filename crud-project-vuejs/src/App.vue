<template>
  <h1>CRUD Project</h1>
  <div class="list">
    <UserCard
      v-for="(user, i) in users"
      :key="i"
      :user="user"
      :index="i"
      v-on:user-changed="changeUser"
      v-on:user-deleted="deleteUser"
    />
  </div>

  <button v-on:click="addNewUser">Add new user</button>
</template>

<script>
import UserCard from "./components/Card.vue";

export default {
  components: {
    UserCard,
  },

  data() {
    return {
      users: [],
    };
  },

  mounted() {
    if (localStorage.users) {
      this.users = JSON.parse(localStorage.users);
    } else {
      this.users = [
        {
          firstName: "Daniel",
          lastName: "Grigore",
          new: false,
        },
        {
          firstName: "Ionescu",
          lastName: "Sorin",
          new: false,
        },
      ];
      localStorage.users = JSON.stringify(this.users);
    }
  },

  methods: {
    changeUser(value, index) {
      this.users[index] = value;
      localStorage.users = JSON.stringify(this.users);
    },

    addNewUser() {
      this.users.push({ name: "", address: "", new: true });
      localStorage.users = JSON.stringify(this.users);
    },

    deleteUser(index) {
      this.users.splice(index, 1);
      localStorage.users = JSON.stringify(this.users);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.list {
  display: flex;
  flex-wrap: wrap;
}
</style>
