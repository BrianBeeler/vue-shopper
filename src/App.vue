<template>
  <div id="app">
    <div id="toggle-container">
      <div>
      <h2>Customer View: <span v-if="!toggleOn">Off</span><span v-if="toggleOn">On</span> </h2>
      <label class="switch">
        <input type="checkbox" v-model="toggleOn">
        <span class="slider round"></span>
      </label>
      </div>
    </div>
    <product-form v-if="!toggleOn" @add:product="addProduct" />
    <product-table v-if="!toggleOn" :products="products" 
      @delete:product="deleteProduct"
      @edit:product="editProduct"
      />
    <customer-table v-if="toggleOn" :products="products" />
  </div>
</template>

<script>
import ProductTable from '@/components/ProductTable.vue'
import ProductForm from '@/components/ProductForm.vue'
import CustomerTable from '@/components/CustomerTable.vue'

export default {
  name: 'App',
  components: {
    ProductTable,
    ProductForm,
    CustomerTable
  },
  data() {
    return {
      products: [
        {
          id: 1,
          name: 'Hyperbaric Oxygen Tank',
          price: '1299',
          purchased: false
        },
        {
          id: 2,
          name: 'Cryogenic Ice Chamber',
          price: '1544',
          purchased: false
        },
        {
          id: 3,
          name: 'Compression Therapy Socks',
          price: '19.99',
          purchased: false
        },
      ],
      toggleOn: true
    }
  },
  methods: {
    addProduct(product) {
      product.purchased = false

      // hack for unique id
      const lastId =
      this.products.length > 0
      ? this.products[this.products.length - 1].id
      : 0;
      const id = lastId + 1;
      const newEmployee = { ...product, id };

      this.products = [...this.products, newEmployee]
    },
    deleteProduct(id) {
      this.products = this.products.filter(
      product => product.id !== id
    )
    },
    editProduct(id, updatedProduct) {
      this.products = this.products.map(product =>
      product.id === id ? updatedProduct : product)
    }
  }
}
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }

  /* The switch - the box around the slider */
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
  margin-left: 100px;
}

/* Hide default HTML checkbox */
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

/* The slider */
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

#toggle-container {
  display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>
