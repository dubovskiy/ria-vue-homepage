<template>
  <table class="table">
    <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col">Name</th>
        <th scope="col">Email</th>
        <th scope="col">Age</th>
      </tr>
    </thead>
    <tbody>
      <UserItem v-for="user in users" v-bind:user="user" :key="user.id" />
    </tbody>
  </table>
</template>

<script>
import UserItem from "@/components/UserItem";
export default {
  name: "UserList",
  props: ["users"],
  components: {
    UserItem,
  },
};
</script>

<style scoped></style>
