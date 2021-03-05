<template>
  <tr>
    <th scope="row">{{ user.id }}</th>
    <td>{{ user.name | capitalize }}</td>
    <td>{{ user.email }}</td>
    <td>{{ user.age }}</td>
  </tr>
</template>

<script>
export default {
  name: "UserItem",
  props: ["user"],
  filters: {
    capitalize(name) {
      return name
        .split(" ")
        .map((nameItem) => nameItem[0].toUpperCase() + nameItem.slice(1))
        .join(" ");
    },
  },
};
</script>

<style scoped></style>
