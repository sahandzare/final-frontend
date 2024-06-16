
<template>
    <div>
      <h2>Sign Up</h2>
      <form @submit.prevent="handleSubmit">
        <div>
          <label for="username">Username:</label>
          <input type="text" id="username" v-model="formData.username" required>
        </div>
        <div>
          <label for="password">Password:</label>
          <input type="password" id="password" v-model="formData.password" required>
        </div>
        <div>
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="formData.email" required>
        </div>
        <button type="submit">Sign Up</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          username: '',
          password: '',
          email: ''
        }
      };
    },
    methods: {
      async handleSubmit() {
        try {
          const response = await fetch('http://localhost:5245/user/signup', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify(this.formData)
          });
          if (response.ok) {
            console.log('User signed up successfully.');
            
          } else {
            console.error('Failed to sign up user.');
            
          }
        } catch (error) {
          console.error('Error signing up user:', error);
          
        }
      }
    }
  };
  </script>
 <style>
 .signup-container {
   max-width: 400px;
   margin: 0 auto;
   padding: 20px;
   background-color: #0edde8;
   border-radius: 8px;
   box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
 }

 h2 {
   font-size: 24px;
   color: #0c9db4;
   margin-bottom: 20px;
   text-align: center;
 }

 form {
   display: flex;
   flex-direction: column;
   align-items: center;
 }

 label {
   font-size: 16px;
   color: #555;
   margin-bottom: 8px;
 }

 input {
   width: 100%;
   padding: 10px;
   margin-bottom: 16px;
   border: 1px solid #06d5e0;
   border-radius: 4px;
   font-size: 16px;
 }

 button {
   width: 100%;
   padding: 12px;
   background-color: #00d9ff;
   color: #fff;
   border: none;
   border-radius: 4px;
   font-size: 18px;
   cursor: pointer;
   transition: background-color 0.3s ease;
 }

 button:hover {
   background-color: #0056b3;
 }
</style>