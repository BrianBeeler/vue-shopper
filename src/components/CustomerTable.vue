<template>
  <div id="employee-table">
    <table>
      <thead>
        <tr>
          <th>Product name</th>
          <th>Product price</th>
          <th>Purchased</th>
        </tr>
      </thead>
      <tbody>
          <tr v-for="employee in employees" :key="employee.id">
            <td v-if="editing === employee.id">
                <input type="text" v-model="employee.name" />
            </td>
            <td v-else>{{employee.name}}</td>
            <td v-if="editing === employee.id">
                <input type="text" v-model="employee.email" />
            </td>
            <td v-else>{{employee.price}}</td>
            <td>
                <button @click="buyItem(employee)" v-if="!employee.purchased">Buy</button>
                <button v-if="employee.purchased">Purchased</button>
            </td>
        </tr>
      </tbody>
    </table>
    <p v-if="employees.length < 1" class="empty-table">No employees</p>
        <table v-else>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'customer-table',
    props: {
        employees: Array
    },
    data() {
        return {
            editing: null
        }
    },
    methods: {
        editMode(id) {
            this.editing = id
        },
        buyItem(employee) {
            employee.purchased = true
            console.log(employee)
        },
        cancelEdit(employee) {
            Object.assign(employee, this.cachedEmployee)
            this.editing = null;
        }
    }
  }
</script>

<style scoped></style>