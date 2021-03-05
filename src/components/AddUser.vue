<template>
  <div>
    <Error v-bind:listErrors="listErrors" />
    <form @submit.prevent="addUser">
      <div class="row g-3">
        <div class="col-sm-5">
          <input
            type="text"
            class="form-control"
            placeholder="Your Name"
            v-model="name"
            @input="(evt) => checkData(evt, 'name')"
          />
        </div>
        <div class="col-sm-5">
          <input
            type="text"
            class="form-control"
            placeholder="Your Email"
            v-model="email"
            @input="(evt) => checkData(evt, 'email')"
          />
        </div>
        <div class="col-sm">
          <input
            type="text"
            class="form-control"
            placeholder="Your Age"
            v-model="age"
            @input="(evt) => checkData(evt, 'age')"
          />
        </div>
      </div>
      <br />
      <div class="col">
        <button type="submit" class="btn btn-primary" :disabled="isDisabled()">
          Add User
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import Error from "@/components/Error";
const validators = {
  name: {
    "Length more than 20 signs": /^.{0,20}$/,
  },
  email: {
    "Wrong Email": /(\w+@[a-zA-Z_]+?\.[a-zA-Z]{2,6})/,
  },
  age: {
    "Is not digit": /^\d*$/,
    "Length more than 3 signs": /^\d{0,3}$/,
  },
};

export default {
  name: "AddUser",
  components: { Error },
  data() {
    return {
      name: "",
      email: "",
      age: "",
      errors: {},
      listErrors: [],
    };
  },
  methods: {
    checkData(evt, fieldName) {
      const validate = validators[fieldName];
      delete this.errors[fieldName];
      this.errors = { ...this.errors };
      for (let errorMsg in validate) {
        if (!validate[errorMsg].test(evt.target.value)) {
          this.errors[fieldName] = errorMsg;
          break;
        }
      }
      this.listErrors = this.getErrorsList(this.errors);
    },
    getErrorsList(errorsObj) {
      const listErrors = [];
      for (let field in errorsObj) {
        listErrors.push(`Field ${field}: ${errorsObj[field]}`);
      }
      return listErrors;
    },
    isDisabled() {
      return (
        Object.entries(this.errors).length ||
        !this.name ||
        !this.age ||
        !this.email
      );
    },
    addUser() {
      const user = {
        name: this.name,
        email: this.email,
        age: this.age,
      };
      this.$emit("addUser", { ...user });
      this.clearData();
    },
    clearData() {
      Object.assign(this, { name: "", email: "", age: "" });
    },
  },
};
</script>

<style scoped></style>
