<template>
  <div class="card">
    <div class="text">
      First Name:
      <div v-if="!editMode">{{ secondUser.firstName }}</div>
      <input v-if="editMode" v-model="secondUser.firstName" />
    </div>
    <div class="text">
      Last Name:
      <div v-if="!editMode">{{ secondUser.lastName }}</div>
      <input v-if="editMode" v-model="secondUser.lastName" />
    </div>

    <button v-on:click="editUser">
      {{ !editMode ? "Edit" : "Save" }}
    </button>
    <button v-on:click="deleteUser">Delete</button>
  </div>
</template>

<script>
export default {
  name: "UserCard",
  props: ["user", "index"],

  methods: {
    editUser() {
      if (this.editMode) {
        this.$emit("user-changed", this.secondUser, this.index);
      }
      this.editMode = !this.editMode;
    },
    deleteUser() {
      this.$emit("user-deleted", this.index);
    },
  },

  data() {
    return {
      editMode: this.user.new ? true : false,
      secondUser: this.user,
    };
  },
};
</script>

<style scoped>
.card {
  border: 1px solid black;
  width: 15%;
  padding: 2% 5%;
  margin: 2% 3%;
  box-shadow: 12px 12px 20px 3px;
  cursor: pointer;
  display: block;
}

.text {
  margin: 0 auto 2% 0;
  text-align: left;
  display: flex;
}

button {
  margin: 0 5%;
}

input {
  width: 50%;
}
</style>
