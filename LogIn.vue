<template>
  <div class="login-container">
    <h2>Log In</h2>
    <form @submit.prevent="handleSubmit">
      <div>
        <label for="username">Username:</label>
        <input type="text" id="username" v-model="formData.username" required>
      </div>
      <div>
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="formData.password" required>
      </div>
      <button type="submit">Log In</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        username: '',
        password: ''
      }
    };
  },
  methods: {
    async handleSubmit() {
      try {
        const response = await fetch('http://localhost:5245/user/login', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(this.formData)
        });
        if (response.ok) {
          console.log("User logged in successfully with user id {}.");
         
        } else {
          console.error('Failed to log in user.');
         
        }
      } catch (error) {
        console.error('Error logging in user:', error);
        
      }
    }
  }
};
</script>

<style>
  .login-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    background-color: #b0faf6;
    border-radius: 8px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  }

  h2 {
    font-size: 24px;
    color: #333;
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
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 16px;
  }

  button {
    width: 100%;
    padding: 12px;
    background-color: #007bff;
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
