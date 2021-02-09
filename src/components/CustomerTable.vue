<template>
  <div id="customer-table">
    <table>
      <thead>
        <tr>
          <th>Product name</th>
          <th>Product price</th>
          <th>Purchased</th>
        </tr>
      </thead>
      <tbody>
          <tr v-for="product in products" :key="product.id">
            <td v-if="editing === product.id">
                <input type="text" v-model="product.name" />
            </td>
            <td v-else>{{product.name}}</td>
            <td v-if="editing === product.id">
                <input type="text" v-model="product.email" />
            </td>
            <td v-else>{{product.price}}</td>
            <td>
                <button @click="buyItem(product)" v-if="!product.purchased">Buy</button>
                <button v-if="product.purchased">Purchased</button>
            </td>
        </tr>
      </tbody>
    </table>
    <p v-if="products.length < 1" class="empty-table">No employees</p>
        <table v-else>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'customer-table',
    props: {
        products: Array
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
        buyItem(product) {
            product.purchased = true
        },
        cancelEdit(employee) {
            Object.assign(employee, this.cachedEmployee)
            this.editing = null;
        }
    }
  }
</script>

<style scoped></style>