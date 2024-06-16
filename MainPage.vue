<template>
  <div class="main-page">
    <HeaderP />
    <FilteringP />
    <div class="camping-spots">
      <h1>Explore Camping Spots</h1>
      <div class="spots-grid">
        <div 
          class="spot-card" 
          v-for="spot in campingSpots" 
          :key="spot.id" 
          :class="{ 'highlighted': spot.availability > 0 }"
          @click="showImages(spot.id)"
        >
          <img :src="getImageUrl(spot.id)" alt=" spot.name " class="spot-image" />
          <div class="spot-details">
            <h2>{{ spot.name }}</h2>
            <p> ID:{{ spot.id }}</p>
            <p>{{ spot.description }}</p>
            <p><strong>Location:</strong> {{ spot.location }}</p>

            <p><strong>Price:</strong> ${{ spot.price }}</p>
            <p><strong>Availability:</strong> {{ spot.availability }} available</p>
          </div>
        </div>
      </div>
    </div>
    <div v-if="selectedSpotImages.length" class="modal" @click="closeModal">
      <div class="modal-content" @click.stop>
        <span class="close" @click="closeModal">&times;</span>
        <div class="images-container">
          <img v-for="(image, index) in selectedSpotImages" :key="index" :src="image" :alt="'Image for spot ' + selectedSpotId" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import FilteringP from '../components/FilteringP.vue';

const images = {
  id1: [require('@/assets/id1/1.jpg'), require('@/assets/id1/2.webp')],
  id2: [require('@/assets/id2/1.jpeg'), require('@/assets/id2/2.webp')],
  id3: [require('@/assets/id3/1.jpeg'), require('@/assets/id3/2.webp')],
  id4: [require('@/assets/id4/1.jpg'), require('@/assets/id4/2.jpg')],
  id5: [require('@/assets/id5/1.jpeg'), require('@/assets/id5/2.jpg')],
  id6: [require('@/assets/id6/1.jpg'), require('@/assets/id6/2.jpg')],
  id7: [require('@/assets/id7/1.jpeg'), require('@/assets/id7/2.jpeg')],
  id8: [require('@/assets/id8/1.jpg'), require('@/assets/id8/2.jpg')],
  id9: [require('@/assets/id9/1.jpeg'), require('@/assets/id9/2.webp')],
  id10: [require('@/assets/id10/1.jpg'), require('@/assets/id10/2.webp')],
};

export default {
  name: 'MainPage',
  components: { FilteringP },
  data() {
    return {
      campingSpots: [],
      selectedSpotId: null,
      selectedSpotImages: [],
    };
  },
  mounted() {
    fetch('http://localhost:5245/CampingSpot')
      .then(response => response.json())
      .then(data => {
        this.campingSpots = data;
      })
      .catch(error => {
        console.error('Error fetching camping spots:', error);
      });
  },
  methods: {
    showImages(spotId) {
      this.selectedSpotId = spotId;
      this.selectedSpotImages = images[`id${spotId}`] || [];
    },
    closeModal() {
      this.selectedSpotId = null;
      this.selectedSpotImages = [];
    },
    getImageUrl(spotId) {
      return images[`id${spotId}`] ? images[`id${spotId}`][0] : 'default_image_path';
    }
  },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

.main-page {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Roboto', sans-serif;
  background-color: #ffffff;
  background-image: url('../assets/pexels-pixabay-219837.jpg');
}

.camping-spots {
  margin-top: 20px;
}

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 40px;
}

.spots-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}

.spot-card {
  background-color: #a4f5f2;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
  cursor: pointer;
}

.spot-card:hover {
  transform: translateY(-20px);
}

.spot-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.spot-details {
  padding: 20px;
}

.spot-details h2 {
  margin: 0 0 10px;
  font-size: 1.5em;
  color: #007BFF;
}

.spot-details p {
  margin: 5px 0;
  color: #555;
}

.spot-details strong {
  color: #333;
}

.highlighted {
  border: 2px solid #007BFF;
}

.modal {
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1000;
}

.modal-content {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  max-width: 90%;
  max-height: 90%;
  overflow-y: auto;
  position: relative;
}

.close {
  position: absolute;
  top: 10px;
  right: 20px;
  font-size: 24px;
  cursor: pointer;
}

.images-container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.images-container img {
  width: 500px;
  height: 500px;
  object-fit: cover;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
</style>