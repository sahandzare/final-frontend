<template>
  <div>
    <h2>Login</h2>
    <form @submit.prevent="login">
      <div>
        <label for="username">Username:</label>
        <input type="text" id="username" v-model="username" required>
      </div>
      <div>
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="password" required>
      </div>
      <button type="submit">Login</button>
    </form>
    
    <!-- Page 1 -->
    <div v-if="currentPage === 'Page1'">
      <OwnerAddSpotPage />
    </div>

    <!-- Page 2 -->
    <div v-if="currentPage === 'Page2'">
      <OwnerSpotOverviewPage />
    </div>
    
    <!-- Navigation buttons -->
    <div v-if="showButtons">
      <button @click="navigateToPage('Page1')">ADD SPOT</button>
      <button @click="navigateToPage('Page2')">OVERVIEW</button>
    </div>
  </div>
</template>

<script>
import OwnerAddSpotPage from './OwnerAddSpotPage.vue';
import OwnerSpotOverviewPage from './OwnerSpotOverviewPage.vue';

export default {
  components: {
    OwnerAddSpotPage,
    OwnerSpotOverviewPage
  },
  data() {
    return {
      username: '',
      password: '',
      showButtons: false,
      currentPage: '' 
    };
  },
  methods: {
    async login() {
      try {
        const response = await fetch('http://localhost:5245/Owner/login', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            username: this.username,
            password: this.password
          })
        });

        if (response.ok) {
          this.showButtons = true; 
        } else {
          console.error('Login failed');
        }
      } catch (error) {
        console.error('Error logging in:', error);
      }
    },
    navigateToPage(page) {
      this.currentPage = page;
    }
  }
};
</script>
