<template>
  <div class="flex items-center justify-center pt-70 shadow-md bg-slate-950 text-white">
    <form @submit.prevent="submitForm">
      <label for="firstname">First Name:</label>
      <input type="text" id="firstname" v-model="firstName" required>

      <label for="lastname">Last Name:</label>
      <input type="text" id="lastname" v-model="lastName" required>

      <label for="department">Department:</label>
      <input type="text" id="department" v-model="Department" required>

      <button type="submit" :disabled="!isvalidFrom">Submit</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      lastName: '',
      firstName: '',
      Department: ''
    };
  },
  computed: {
    isvalidFrom() {
      return this.firstName && this.lastName && this.Department;
  }
},
  methods: {
    async submitForm() {
      try {
        const formData = {
          firstname: this.firstName,
          lastname: this.lastName,
          department: this.Department
        };

        const response = await axios.post('http://localhost:8080/api', formData);

        console.log(response.status);
        console.log('Form submitted successfully!!', response.data);
        this.$router.push('/');
        
      } catch (error) {
        console.error('Error submitting form:', error.response ? error.response.data : error.message);
      }
    }
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

label {
  display: block;
  margin-bottom: 8px;
  font-weight: bold;
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
}

button {
  width: 100%;
  padding: 10px;
  background-color: limegreen;
  border: none;
  border-radius: 4px;
  color: white;
  font-size: 16px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>
