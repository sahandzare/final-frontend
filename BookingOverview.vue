<template>
    <div class="booking-overview-page">
      <h2>Booking Overview</h2>
      <form @submit.prevent="fetchUserBookings" class="form">
        <div class="form-group">
          <label for="username">Username:</label>
          <input type="text" id="username" v-model="credentials.username" required>
        </div>
        <div class="form-group">
          <label for="password">Password:</label>
          <input type="password" id="password" v-model="credentials.password" required>
        </div>
        <button type="submit" class="btn">See Your Bookings</button>
      </form>
      <div v-if="userBookings.length > 0" class="booking-list">
        <h3>Your Bookings:</h3>
        <ul>
          <li v-for="booking in userBookings" :key="booking.bookingId" class="booking-item">
            <p><strong>Booking ID:</strong> {{ booking.bookingId }}</p>
            <p><strong>Camping Spot ID:</strong> {{ booking.campingSpotId }}</p>
            <p><strong>Check-In Date:</strong> {{ formatDate(booking.checkInDate) }}</p>
            <p><strong>Check-Out Date:</strong> {{ formatDate(booking.checkOutDate) }}</p>
          </li>
        </ul>
      </div>
      <div v-else-if="loading" class="loading">
        <p>Loading...</p>
      </div>
      <div v-if="error" class="error">
        <p>{{ error }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        credentials: {
          username: '',
          password: ''
        },
        userBookings: [],
        loading: false,
        error: ''
      };
    },
    methods: {
      async fetchUserBookings() {
        try {
          this.loading = true;
          this.error = '';
  
          const username = this.credentials.username;
          const password = this.credentials.password;
  
          const response = await fetch('http://localhost:5245/Booking/BookingsOverview', {
            headers: {
              'Username': username,
              'Password': password
            }
          });
  
          if (response.ok) {
            const data = await response.json();
            this.userBookings = data;
          } else {
            const errorMessage = await response.text();
            this.error = errorMessage;
          }
        } catch (error) {
          console.error('Error fetching user bookings:', error);
          this.error = 'Failed to fetch user bookings. Please try again later.';
        } finally {
          this.loading = false;
        }
      },
      formatDate(date) {
        return new Date(date).toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
      }
    }
  };
  </script>
  
  <style scoped>
  .booking-overview-page {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
  }
  
  .form {
    margin-bottom: 20px;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
  }
  
  input[type="text"],
  input[type="password"] {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #2ec7de;
    border-radius: 4px;
  }
  
  .btn {
    padding: 10px 20px;
    font-size: 16px;
    background-color: #25b5ea;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .btn:hover {
    background-color: #0056b3;
  }
  
  .booking-list {
    margin-top: 20px;
  }
  
  .booking-item {
    background-color: #cbdeec;
    border: 1px solid #ddd;
    border-radius: 4px;
    padding: 15px;
    margin-bottom: 10px;
  }
  
  .error {
    color: #dc3545;
    margin-top: 10px;
  }
  
  .loading {
    margin-top: 20px;
    font-style: italic;
  }
  </style>
  