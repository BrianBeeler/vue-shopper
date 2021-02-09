<template>
  <form @submit.prevent="handleSubmit">
  <label>Product name</label>
  <input
    ref="first"
    type="text"
    :class="{ 'has-error': submitting && invalidName }"
    v-model="employee.name"
    @focus="clearStatus"
    @keypress="clearStatus"
  />
  <label>Employee Price</label>
  <input
    type="text"
    :class="{ 'has-error': submitting && invalidEmail }"
    v-model="employee.price"
    @focus="clearStatus"
  />
  <p v-if="error && submitting" class="error-message">
    ❗Please fill out all required fields
  </p>
  <p v-if="success" class="success-message">✅ Employee successfully added</p>
  <button>Add Product</button>
</form>
</template>

<script>
  export default {
    name: 'employee-form',
    data() {
      return {
        submitting: false,
        error: false,
        success: false,
        employee: {
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

            this.$emit('add:employee', this.employee)
            this.employee = {
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
            return this.employee.name === ''
        },
        invalidEmail() {
            return this.employee.price === ''
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