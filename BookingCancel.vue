<template>
    <div>
      <h2>Cancel Booking</h2>
      <form @submit.prevent="cancelBooking">
        <div>
          <label for="bookingId">Booking ID:</label>
          <input type="text" id="bookingId" v-model="bookingId" required>
        </div>
        <button type="submit">Cancel Booking</button>
      </form>
      <div v-if="cancellationResult" class="result">
        <p>{{ cancellationResult }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        bookingId: '',
        cancellationResult: ''
      };
    },
    methods: {
      async cancelBooking() {
        try {
          const response = await fetch(`http://localhost:5245/Booking/cancel/${this.bookingId}`, {
            method: 'DELETE'
          });
  
          if (response.ok) {
            this.cancellationResult = 'Booking canceled successfully.';
          } else {
            this.cancellationResult = 'Failed to cancel booking.';
          }
        } catch (error) {
          console.error('Error canceling booking:', error);
          this.cancellationResult = 'Error canceling booking. Please try again later.';
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .result {
    margin-top: 20px;
    border: 1px solid #ccc;
    padding: 10px;
    text-align: center;
    font-weight: bold;
    font-size: 20px;
    background-color: aqua;
  }
  </style>
  