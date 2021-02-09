<template>
  <div id="employee-table">
    <table>
      <thead>
        <tr>
          <th>Product name</th>
          <th>Product price</th>
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
            <td v-if="editing === product.id">
                <button @click="editEmployee(product)">Save</button>
                <button class="muted-button" @click="editing = null">Cancel</button>
            </td>
            <td v-else>
                <button @click="editMode(product.id)">Edit</button>
                <button @click="$emit('delete:product', product.id)">Delete</button>
            </td>
        </tr>
      </tbody>
    </table>
    <p v-if="products.length < 1" class="empty-table">No Products or Services</p>
        <table v-else>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'product-table',
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
        editProduct(product) {
            if (product.name === '' || product.email === '') return
            this.$emit('edit:product', product.id, product)
            this.editing = null
        },
        cancelEdit(product) {
            Object.assign(product, this.cachedProduct)
            this.editing = null;
        }
    }
  }
</script>

<style scoped></style>