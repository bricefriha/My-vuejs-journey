<template>
  <div id="app" class="small-container">
    <!-- Header Title -->
    <h1>Employees</h1>
    <!-- Import our add form -->
    <employee-form @add:employee="addEmployee" />
    <!-- Import our table -->
    <employee-table :employees="employees" @delete:employee="deleteEmployee"/>
  </div>
</template>

<script>
// Importing the EmployeeTable view
import EmployeeTable  from '@/components/EmployeeTable.vue'

// Importing the EmployeeTable view
import EmployeeForm from '@/components/EmployeeForm.vue'

export default {
  name: 'app',
  components: {
    EmployeeTable,
    EmployeeForm,
  },

// All the methods
methods: {
  // Function to delete a employee
  deleteEmployee(id) {
    // Get all employees except the one we want to delete
    this.employees = this.employees.filter(
      employee => employee.id !== id
    );
  },

  // Add a new employee
  addEmployee(employee) {

    // Get the last 
    const lastId = this.employees.length > 0
                    ? this.employees[this.employees.length - 1].id
                    : 0;

    // Set a new id for the employee 
    const id = lastId + 1;

    // Set the new employe as a object
    const newEmployee = { ...employee, id };

    // Reload the employee list with the new employe 
    this.employees = [...this.employees, newEmployee]
  }
},
  
data() {
    
    return {
      employees: [
        {
          id: 1,
          name: 'Richard Hendricks',
          email: 'richard@piedpiper.com',
        },
        {
          id: 2,
          name: 'Bertram Gilfoyle',
          email: 'gilfoyle@piedpiper.com',
        },
        {
          id: 3,
          name: 'Dinesh Chugtai',
          email: 'dinesh@piedpiper.com',
        },
      ],
    }
  },
}

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
button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>
