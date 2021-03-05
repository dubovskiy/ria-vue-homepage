<template>
  <div v-show="listErrors.length" class="alert alert-danger" role="alert">
    <div v-for="error in listErrors" :key="error">
      <div>{{ error }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Error",
  props: ["listErrors"],
};
</script>

<style scoped></style>
