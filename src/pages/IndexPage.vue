<template>
  <q-page class="q-pa-md flex flex-center">
    <q-card class="q-pa-lg shadow-2 rounded-borders" style="width: 400px;">

      <q-card-section>
        <div class="text-h6 text-center">Basic Form</div>
      </q-card-section>

      <q-form
        ref="formRef"
        @submit.prevent="onSubmit"
        @reset="onReset"
        class="q-gutter-md"
      >
        <q-input
          filled
          v-model="form.name"
          label="Name"
          :rules="[val => !!val || 'Name is required']"
        />

        <q-input
          filled
          v-model="form.email"
          label="Email"
          type="email"
          :rules="[
            val => !!val || 'Email is required',
            val => /.+@.+\..+/.test(val) || 'Email must be valid'
          ]"
        />

        <q-input
          filled
          v-model="form.password"
          label="Password"
          type="password"
          :rules="[val => val && val.length >= 6 || 'Minimum 6 characters']"
        />

        <div class="row justify-center q-gutter-sm">
          <q-btn label="Submit" type="submit" color="primary" />
          <q-btn label="Reset" type="reset" color="secondary" flat />
        </div>
      </q-form>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'

const formRef = ref(null)

const form = ref({
  name: '',
  email: '',
  password: ''
})

function onSubmit() {
  formRef.value.validate().then(success => {
    if (success) {
      alert(`Form submitted!\nName: ${form.value.name}\nEmail: ${form.value.email}`)
    } else {
      alert('Please fill out all required fields correctly.')
    }
  })
}

function onReset() {
  form.value.name = ''
  form.value.email = ''
  form.value.password = ''
  formRef.value.resetValidation()
}
</script>
