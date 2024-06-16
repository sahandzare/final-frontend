<template>
    <div class="booking-page">
      <h2>Book Camping Spot</h2>
      <form @submit.prevent="bookSpot">
        <div>
          <label for="userId">User ID:</label>
          <input type="text" id="userId" v-model="formData.userId" required>
        </div>
        <div>
          <label for="campingSpotId">Camping Spot ID:</label>
          <input type="text" id="campingSpotId" v-model="formData.campingSpotId" required>
        </div>
        <div>
          <label for="checkInDate">Check-In Date:</label>
          <input type="date" id="checkInDate" v-model="formData.checkInDate" required>
        </div>
        <div>
          <label for="checkOutDate">Check-Out Date:</label>
          <input type="date" id="checkOutDate" v-model="formData.checkOutDate" required>
        </div>
        <button type="submit">Book</button>
      </form>
      <div v-if="bookingId !== null" class="popup">
        <p>Spot booked successfully. Your booking ID is {{ bookingId }}.</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          userId: '',
          campingSpotId: '',
          checkInDate: '',
          checkOutDate: ''
        },
        bookingId: null,
        campingSpot: {}, 
      };
    },
    mounted() {
      
      fetch('http://localhost:5245/CampingSpot') 
        .then(response => response.json())
        .then(data => {
         
          this.campingSpot = data[0];
        })
        .catch(error => {
          console.error('Error fetching camping spot:', error);
        });
    },
    methods: {
      async bookSpot() {
        try {
         
          if (this.campingSpot.availability <= 0) {
            console.error('Spot is not available.');
            return; 
          }
  
          const response = await fetch('http://localhost:5245/Booking/book', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify(this.formData)
          });
  
          if (response.ok) {
            const data = await response.json();
            this.bookingId = data.bookingId;
          } else {
            console.error('Failed to book the spot.');
          }
        } catch (error) {
          console.error('Error booking spot:', error);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .booking-page {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
  }
  
  form {
    margin-bottom: 20px;
  }
  
  .popup {
    background-color: #f0f0f0;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }
  </style>
  