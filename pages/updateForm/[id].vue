<template>
  <div class="flex items-center justify-center pt-70 shadow-md bg-slate-950 text-white">
    <form @submit.prevent="updateInfo">
      <h1>UPDATE FORM</h1>
      <label for="firstname">First Name:</label>
      <input type="text" id="firstname" v-model="firstname" required>

      <label for="lastname">Last Name:</label>
      <input type="text" id="lastname" v-model="lastname" required>

      <label for="department">Department:</label>
      <input type="text" id="department" v-model="Department" required>

      <button type="submit">UPDATE</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import axios from 'axios';

const route = useRoute();
const id = route.params.id;

const lastname = ref('');
const firstname = ref('');
const Department = ref('');

const router = useRouter();

const updateInfo = async () => {
  try {
    const formData = {
      firstname: firstname.value,
      lastname: lastname.value,
      dept: Department.value
    };

    const response = await axios.put(`http://localhost:8080/api/${id}`, formData);
    console.log(response.status);
    console.log('Form updated successfully!', response.data);
    router.push('/');

  } catch (error) {
    console.error('Error submitting form:', error);
  }
};
</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  background-color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

.flex.items-center.justify-center.pt-70.shadow-md.bg-slate-950 {
  height: calc(100vh - 0px); /* Adjust height as needed */
}

form {
  box-shadow: 0 10px 30px rgb(255, 255, 255);
  background: transparent;
  padding: 40px;
  border-radius: 8px;
  width: 100%;
  max-width: 400px;
}

h1 {
  text-align: center;
  color: #fff; /* White text color */
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  font-weight: bold;
  font-size: 16px;
  color: #ddd; /* Light grey text color */
}

input[type="text"] {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  font-size: 16px;
  color: black;
  background-color: #fff; /* White background for input fields */
}

button[type="submit"] {
  width: 100%;
  padding: 10px;
  background-color: limegreen;
  border: none;
  border-radius: 4px;
  color: white;
  font-size: 16px;
  cursor: pointer;
}

button[type="submit"]:hover {
  background-color: #0056b3;
}
</style>
