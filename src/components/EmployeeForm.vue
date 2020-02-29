<template>
  <div id="employee-form" @submit.prevent="handleSubmit" class="form">
    <form>
      <label>Employee name</label>
      <input v-model="employee.name" type="text" />
      <label>Employee Email</label>
      <input v-model="employee.email" type="text" />
      <button class="">Add Employee</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'employee-form',
        data() {
        return {
            employee: {
            name: '',
            email: '',
            },
        }
        },
    methods: {
        handleSubmit() {
        // Passing the employee info
        this.$emit('add:employee', this.employee);
        },
    },
  }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }
</style>