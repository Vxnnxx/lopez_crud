<template>
  <div class="container mx-auto bg-slate-950">
    <div class="w-32 h-32 rounded-xl bg-slate-950"></div>
    <h2 class="text-2xl font-bold mb-4 text-center text-white">Student List</h2>
    <div class="flex justify-end mb-4">
      <button @click="navigateTo('/new')" class="bg-green-600 text-white py-2 px-4 rounded-lg hover:bg-green-700">Add Student</button>
    </div>
    <table class="w-full border-collapse border border-white-200 mt-4">
      <thead>
        <tr class="bg-black text-white">
          <th class="border border-white">ID</th>
          <th class="border border-white">Firstname</th>
          <th class="border border-white">Lastname</th>
          <th class="border border-white">Department</th>
          <th class="border border-white">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, index) in users" :key="index" class="hover:bg-white-100">
          <td class="border border-white text-white">{{ user.ID }}</td>
          <td class="border border-white text-white">{{ user.fname }}</td>
          <td class="border border-white text-white">{{ user.lname }}</td>
          <td class="border border-white text-white">{{ user.Department }}</td>
          <td class="border border-white text-white">
            <button @click="navigateToUpdateForm(user.ID)" class="bg-blue-600 text-white py-2 px-4 rounded-lg hover:bg-blue-700">Edit</button>
            <button @click="deleteUser(user.ID)" class="bg-red-600 text-white py-2 px-4 rounded-lg hover:bg-red-700">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      users: []
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    async getData() {
      try {
        const response = await axios.get('http://localhost:8080/api/load'); 
        this.users = response.data;
      } catch (error) {
        console.error('Error making GET request:', error);
      }
    },
    navigateToUpdateForm(id) {
      this.$router.push(`/updateForm/${id}`);
    },
    async deleteUser(userId) {
      try {
        await axios.delete(`http://localhost:8080/api/${userId}`);
        this.users = this.users.filter(user => user.ID !== userId);
      } catch (error) {
        console.error('Error deleting user:', error);
      }
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 3000px;  /* Optional: Maintain a maximum width */
  margin: 0 auto;
  min-height: 100vh;  /* Set container minimum height to 100% viewport height */
  display: flex;
  flex-direction: column;
  background-color: #020617;
}
</style>
