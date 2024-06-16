<template>
  <div>
    <h2>Add New Camping Spot</h2>
    <form @submit.prevent="addSpot">
      <label for="name">Name:</label>
      <input type="text" id="name" v-model="campingSpot.Name" required>
      <label for="description">Description:</label>
      <textarea id="description" v-model="campingSpot.Description" required></textarea>
      <label for="location">Location:</label>
      <input type="text" id="location" v-model="campingSpot.Location" required>
      <label for="price">Price:</label>
      <input type="number" id="price" v-model.number="campingSpot.Price" required>
      <label for="availability">Availability:</label>
      <input type="number" id="availability" v-model.number="campingSpot.Availability" required>
      <button type="submit">Add Spot</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      campingSpot: {
        Name: '',
        Description: '',
        Location: '',
        Price: 0,
        Availability: 0 
      }
    };
  },
  methods: {
    async addSpot() {
      try {
        const response = await fetch('http://localhost:5245/owner/addspot', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(this.campingSpot)
        });

        if (response.ok) {
          const responseData = await response.json();
          console.log(responseData);
        } else {
          console.error('Adding spot failed');
        }
      } catch (error) {
        console.error('Error adding spot:', error);
      }
    }
  }
};
</script>
