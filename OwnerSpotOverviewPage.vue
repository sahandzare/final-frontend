<template>
  <div class="spot-overview">
    <h2 class="title">Camping Spot Overview</h2>
    <div v-for="spot in spots" :key="spot.id" class="spot">
      <h3 class="spot-name">{{ spot.name }}</h3>
      <p class="spot-description">Description: {{ spot.description }}</p>
      <p class="spot-price">Price: {{ spot.price }}</p>
      <p class="spot-availability">Availability: {{ spot.availability }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      spots: []
    };
  },
  created() {
    this.fetchSpots();
  },
  methods: {
    async fetchSpots() {
      try {
        
        const response = await fetch('http://localhost:5245/owner/spots');
        if (response.ok) {
          this.spots = await response.json();
        } else {
          console.error('Failed to fetch spots:', response.statusText);
     
        }
      } catch (error) {
        console.error('Error fetching spots:', error);
       
      }
    }
  }
};
</script>

<style scoped>
.spot-overview {
  margin: 20px;
}

.title {
  font-size: 24px;
  margin-bottom: 10px;
}

.spot {
  border: 1px solid #ccc;
  padding: 10px;
  margin-bottom: 10px;
}

.spot-name {
  font-size: 20px;
  margin-bottom: 5px;
}

.spot-description,
.spot-price,
.spot-availability {
  margin-bottom: 5px;
}
</style>
