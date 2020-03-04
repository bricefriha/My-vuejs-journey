<template>
  <div id="employee-table">
    <p v-if="employees.length < 1" class="empty-table">No employees</p>
    <table v-else>
      <thead>
        <tr>
          <th>Employee name</th>
          <th>Employee email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" :key="employee.id">
          <!-- only in edit mode -->
          <td v-if="editing === employee.id">
            <!--edit input name-->
            <input type="text" v-model="employee.name" />
          </td>
          <!-- Otherwise on display mode-->
          <td v-else>{{ employee.name }}</td>
          <!-- only in edit mode -->
          <td v-if="editing === employee.id">
            <!--edit input email-->
            <input type="text" v-model="employee.email" />
          </td>
          <!-- Otherwise on display mode-->
          <td v-else>{{ employee.email }}</td>
          <!-- only in edit mode -->
          <td v-if="editing === employee.id">
            <button @click="editEmployee(employee)">Save</button>
            <button class="muted-button" @click="editing = null">Cancel</button>
          </td>
          <!-- Otherwise-->
          <td v-else>
            <!-- Button to edit an employe -->
            <button @click="editMode(employee.id)">Edit</button>
            <!-- Button to delete an employe -->
            <button @click="$emit('delete:employee', employee.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "employee-table",
  props: {
    employees: Array
  },

  data() {
    return {
      editing: null
    };
  },
  methods: {
    editMode(id) {
      this.editing = id;
    },

    // Method to cancel an editing
    cancelEdit(employee) {
      Object.assign(employee, this.cachedEmployee);
      this.editing = null;
    },
    // Method to edit an employe
    editEmployee(employee) {
      if (employee.name === "" || employee.email === "")
        return this.$emit("edit:employee", employee.id, employee);

      this.editing = null;
    }
  }
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
button {
  margin: 0 0.5rem 0 0;
}
</style>