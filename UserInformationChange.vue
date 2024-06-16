<template>
    <div>
      <h2>Update User Information</h2>
      <form @submit.prevent="updateUser">
        <div>
          <label for="currentUsername">Current Username:</label>
          <input type="text" id="currentUsername" v-model="formData.currentUsername" required>
        </div>
        <div>
          <label for="currentPassword">Current Password:</label>
          <input type="password" id="currentPassword" v-model="formData.currentPassword" required>
        </div>
        <div>
          <label for="newEmail">New Email:</label>
          <input type="email" id="newEmail" v-model="formData.newEmail">
        </div>
        <div>
          <label for="newPassword">New Password:</label>
          <input type="password" id="newPassword" v-model="formData.newPassword">
        </div>
        <div>
          <label for="newUsername">New Username:</label>
          <input type="text" id="newUsername" v-model="formData.newUsername">
        </div>
        <button type="submit">Update</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          currentUsername: '',
          currentPassword: '',
          newEmail: '',
          newPassword: '',
          newUsername: ''
        }
      };
    },
    methods: {
      async updateUser() {
        try {
          const response = await fetch('http://localhost:5245/User/update', {
            method: 'PUT',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify(this.formData)
          });
  
          if (response.ok) {
            console.log('User details updated successfully.');
          } else {
            console.error('Failed to update user information:', response.statusText);
          }
        } catch (error) {
          console.error('Error updating user information:', error);
        }
      }
    }
  };
  </script>
  