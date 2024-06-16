<template>
  <div class="filter-container">
    <div class="filter-inputs">
      <label for="location">Location:</label>
      <input type="text" id="location" v-model="location">
      <br>

      <label for="minPrice">Minimum Price:</label>
      <input type="number" id="minPrice" v-model.number="minPrice">
      <br>

      <label for="maxPrice">Maximum Price:</label>
      <input type="number" id="maxPrice" v-model.number="maxPrice">
      <br>

      <button @click="fetchFilteredCampingSpots">Filter</button>
    </div>
    
    <div class="error-message" v-if="errorMessage">{{ errorMessage }}</div>

    <div class="camping-spot" v-for="spot in campingSpots" :key="spot.id">
      <h3>{{ spot.name }}</h3>
      <p>ID:{{ spot.id }}</p>
      <p>Location: {{ spot.location }}</p>
      <p>Description: {{ spot.description }}</p>
      <p>Price: {{ spot.price }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      location: '',
      minPrice: 0,
      maxPrice: 1000,
      campingSpots: [],
      errorMessage: ''
    };
  },
  methods: {
    async fetchFilteredCampingSpots() {
      try {
        const response = await fetch(`http://localhost:5245/campingspot/filter?location=${this.location}&minPrice=${this.minPrice}&maxPrice=${this.maxPrice}`);
        if (response.ok) {
          this.campingSpots = await response.json();
          if (this.campingSpots.length === 0) {
            this.errorMessage = `Sorry, there are no spots in the location '${this.location}'.`;
          } else {
            this.errorMessage = '';
          }
        } else {
          console.error('Failed to fetch filtered camping spots.');
        }
      } catch (error) {
        console.error('Error fetching filtered camping spots:', error);
      }
    }
  }
};
</script>

<style scoped>
.filter-container {
  max-width: 600px;
  margin: 0 auto;
}

.filter-inputs {
  margin-bottom: 20px;
}

.error-message {
  color: red;
  font-weight: bold;
}

.camping-spot {
  border: 1px solid #46b1c7;
  padding: 10px;
  margin-bottom: 10px;
  background-color: aqua;
}
</style>
