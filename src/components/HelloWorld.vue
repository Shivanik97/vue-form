<template>
  <form @submit.prevent="submitForm" style="max-width: 600px; margin: 0 auto; ">
    <div style="border:#007bff;">
      <label style="display: block; margin-bottom: 10px;">
        First name:
        <input type="text" v-model="formData.name.firstName" required
          style="padding: 5px; border-radius: 3px; border: 1px solid #ccc;">
      </label>
      <label style="display: block; margin-bottom: 10px;">
        Last name:
        <input type="text" v-model="formData.name.lastName" required
          style="padding: 5px; border-radius: 3px; border: 1px solid #ccc;">
      </label>
      <label style="display: block; margin-bottom: 10px;">
        Email:
        <input type="email" v-model="formData.email" required
          style="padding: 5px; border-radius: 3px; border: 1px solid #ccc;">
      </label>
      <label style="display: block; margin-bottom: 10px;">
        Phone:
        <input type="tel" v-model="formData.phone" required
          style="padding: 5px; border-radius: 3px; border: 1px solid #ccc;">
      </label>
      <label style="display: block; margin-bottom: 10px;">
        Street:
        <input type="text" v-model="formData.address.street" required
          style="padding: 5px; border-radius: 3px; border: 1px solid #ccc;">
      </label>
      <label style="display: block; margin-bottom: 10px;">
        City:
        <input type="text" v-model="formData.address.city" required
          style="padding: 5px; border-radius: 3px; border: 1px solid #ccc;">
      </label>
      <label style="display: block; margin-bottom: 10px;">
        State:
        <input type="text" v-model="formData.address.state" required
          style="padding: 5px; border-radius: 3px; border: 1px solid #ccc;">
      </label>
      <label style="display: block; margin-bottom: 10px;">
        Postal code:
        <input type="number" v-model="formData.address.postalCode" required
          style="padding: 5px; border-radius: 3px; border: 1px solid #ccc;">
      </label>
      <label style="display: block; margin-bottom: 10px;">
        Years of work experience:
        <input type="number" v-model="formData.workExperience.years" required
          style="padding: 5px; border-radius: 3px; border: 1px solid #ccc;">
      </label>
      <label style="display: block; margin-bottom: 10px;">
        Months of work experience:
        <input type="number" v-model="formData.workExperience.months" required
          style="padding: 5px; border-radius: 3px; border: 1px solid #ccc;">
      </label>
      <label style="display: block; margin-bottom: 10px;">
        Status:
        <input type="text" v-model="formData.status.value" required
          style="padding: 5px; border-radius: 3px; border: 1px solid #ccc;">
      </label>
      <button type="submit"
        style="background-color: #007bff; color: #fff; border: none; padding: 10px 20px; border-radius: 3px; cursor: pointer;">Submit</button>
    </div>
  </form>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';

interface Name {
  firstName: string;
  lastName: string;
}
interface Address {
  street: string;
  city: string;
  state: string;
  postalCode: number;
}

interface WorkExperience {
  years: number;
  months: number;
}

interface Status {
  value: string;
}

interface FormData {
  name: Name;
  email: string;
  phone: string;
  address: Address;
  workExperience: WorkExperience;
  status: Status;
}

const formData = ref<FormData>({
  name: {
    firstName: '',
    lastName: '',
  },
  email: '',
  phone: '',
  address: {
    street: '',
    city: '',
    state: '',
    postalCode: 0,
  },
  workExperience: {
    years: 0,
    months: 0,
  },
  status: {
    value: '',
  },
});

async function submitForm() {
  try {
    const { name, email, phone, address, workExperience, status } = formData.value
    console.log(formData.value)
    const data = { name, email, phone, address, workExperience, status }
    const response = await axios.post('https://shravanariqtportaldemo-web-dev.azurewebsites.net/api/Candidate', data)
    console.log(response)
  }
  catch (error: any) {
    console.error(error)
  }
}
</script>
<style>
/* Add additional styles in this block */
label {
  display: block;
  margin-bottom: 10px;
}

input[type="text"],
input[type="email"],
input[type="tel"],
input[type="number"],
input[type="password"],
textarea {
  padding: 5px;
  border-radius: 3px;
  border: 1px solid #ccc;
}

button[type="submit"] {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 3px;
  cursor: pointer;
}
</style>