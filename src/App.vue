<template>
  <div id="app" class="small-container">
    <!-- Header Title -->
    <h1>Employees</h1>
    <!-- Import our add form -->
    <employee-form @add:employee="addEmployee" />
    <!-- Import our table -->
    <employee-table :employees="employees" 
                    @delete:employee="deleteEmployee"
                    @edit:employee="editEmployee"/>
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
  async deleteEmployee(id) {
    try {
      await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
        method: "DELETE"
      });
      this.employees = this.employees.filter(employee => employee.id !== id);
    } catch (error) {
      console.error(error);
    }
  },
  // deleteEmployee(id) {
  //   // Get all employees except the one we want to delete
  //   this.employees = this.employees.filter(
  //     employee => employee.id !== id
  //   );
  // },
  // Function to edit an employee
  async editEmployee(id, updatedEmployee) {
    try {
      const response = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
        method: 'PUT',
        body: JSON.stringify(updatedEmployee),
        headers: { 'Content-type': 'application/json; charset=UTF-8' },
      })
      const data = await response.json()
      this.employees = this.employees.map(employee => (employee.id === id ? data : employee))
    } catch (error) {
      console.error(error)
    }
  },
  // editEmployee(id, updatedEmployee) {
  //   this.employees = this.employees.map(employee =>
  //     employee.id === id ? updatedEmployee : employee
  //   )
  // },

  // Add a new employee
  async addEmployee(employee) {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/users', {
        method: 'POST',
        body: JSON.stringify(employee),
        headers: { 'Content-type': 'application/json; charset=UTF-8' },
      })
      const data = await response.json()
      this.employees = [...this.employees, data]
    } catch (error) {
      console.error(error)
    }
  },
  // addEmployee(employee) {

  //   // Get the last 
  //   const lastId = this.employees.length > 0
  //                   ? this.employees[this.employees.length - 1].id
  //                   : 0;

  //   // Set a new id for the employee 
  //   const id = lastId + 1;

  //   // Set the new employe as a object
  //   const newEmployee = { ...employee, id };

  //   // Reload the employee list with the new employe 
  //   this.employees = [...this.employees, newEmployee]
  // },
  // Get all employees
  async getEmployees() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users')
    const data = await response.json()
    this.employees = data
  } catch (error) {
    console.error(error)
  }
}
  
},
  
data() {
    
    return {
      employees: [
        // {
        //   id: 1,
        //   name: 'Richard Hendricks',
        //   email: 'richard@piedpiper.com',
        // },
        // {
        //   id: 2,
        //   name: 'Bertram Gilfoyle',
        //   email: 'gilfoyle@piedpiper.com',
        // },
        // {
        //   id: 3,
        //   name: 'Dinesh Chugtai',
        //   email: 'dinesh@piedpiper.com',
        // },
      ],
    }
  },
   mounted() {
    this.getEmployees()
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
