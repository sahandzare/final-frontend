<template>
  <div class="booking-page">
    
    <BookingP />
  </div>
</template>

<script>

import BookingP from '../components/BookingP.vue';

export default {
  name: 'BookingPage',
  components: {
  
    BookingP,
  },
};
</script>

<style scoped>
.booking-page {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}
</style>
