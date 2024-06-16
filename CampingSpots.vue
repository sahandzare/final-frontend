<template>
    <div>
      
      <ul>
        <li v-for="spot in spots" :key="spot.id">
          <h3>{{ spot.name }}</h3>
          <p>{{ spot.location }}</p>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CampingSpots',
    data() {
      return {
        spots: []
      }
    }
  }
  </script>
  
  <style scoped>
 
  </style>
