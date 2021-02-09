<template>
  <form @submit.prevent="handleSubmit">
  <label>Product name</label>
  <input
    ref="first"
    type="text"
    :class="{ 'has-error': submitting && invalidName }"
    v-model="product.name"
    @focus="clearStatus"
    @keypress="clearStatus"
  />
  <label>Product Price</label>
  <input
    type="text"
    :class="{ 'has-error': submitting && invalidEmail }"
    v-model="product.price"
    @focus="clearStatus"
  />
  <p v-if="error && submitting" class="error-message">
    ❗Please fill out all required fields
  </p>
  <p v-if="success" class="success-message">✅ Product successfully added</p>
  <button>Add Product</button>
</form>
</template>

<script>
  export default {
    name: 'product-form',
    data() {
      return {
        submitting: false,
        error: false,
        success: false,
        product: {
          name: '',
          price: '',
        },
      }
    },
    methods: {
        handleSubmit() {
            this.submitting = true
            this.clearStatus()

            if (this.invalidName || this.invalidPrice) {
                this.error = true
                return
            }

            this.$emit('add:product', this.product)
            this.product = {
                name: '',
                price: ''
            }
            this.error = false
            this.success = true
            this.submitting = false
            this.$refs.first.focus()
        },
        clearStatus() {
            this.success = false
            this.error = true
        }
    },
    computed: {
        invalidName() {
            return this.product.name === ''
        },
        invalidEmail() {
            return this.product.price === ''
        }
    }
  }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }

</style>