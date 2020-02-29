<template>
  <div id="employee-form" @submit.prevent="handleSubmit">
    <form>
      <label>Employee name</label>
      <input
        type="text"
        :class="{ 'has-error': submitting && invalidName }"
        v-model="employee.name"
        @focus="clearStatus"
        @keypress="clearStatus"
      />
      <label>Employee Email</label>
      <input
        v-model="employee.email"
        type="text"
        :class="{ 'has-error': submitting && invalidEmail }"
        @focus="clearStatus"
      />
      <!-- Error message -->
      <p v-if="error && submitting" class="error-message">❗Please fill out all required fields</p>
      <!-- Success message -->
      <p v-if="success" class="success-message">✅ Employee successfully added</p>
      <button>Add Employee</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "employee-form",
  data() {
    return {
      employee: {
        name: "",
        email: ""
      }
    };
  },
  methods: {
    handleSubmit() {
      this.submitting = true;

      // Clear the status
      this.clearStatus();

      //
      if (this.invalidName || this.invalidEmail) {
        this.error = true;
        return;
      }
      // Passing the employee info
      this.$emit("add:employee", this.employee);

      this.employee = {
        name: "",
        email: ""
      };
      this.error = false;
      this.success = true;
      this.submitting = false;
    },
    clearStatus() {
      this.success = false;
      this.error = false;
    }
  },
  computed: {
    invalidName() {
      return this.employee.name === "";
    },

    invalidEmail() {
      return this.employee.email === "";
    },
    data() {
      return {
        submitting: false,
        error: false,
        success: false,
        employee: {
          name: "",
          email: ""
        }
      };
    }
  }
};
</script>

<style scoped>
form {
  margin-bottom: 2rem;
}
form {
  margin-bottom: 2rem;
}

[class*="-message"] {
  font-weight: 500;
}

.error-message {
  color: #d33c40;
}

.success-message {
  color: #32a95d;
}
</style>