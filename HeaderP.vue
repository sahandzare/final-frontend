<template>
  <header>

  </header>
</template>

<script>
export default {
  name: 'HeaderP'
};
</script>



<style scoped>
.header {
  background-color: #333;
  padding: 10px 20px;
  color: white;
}

.nav {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

.nav li {
  display: inline;
  margin-right: 10px;
}

.nav li:last-child {
  margin-right: 0;
}
</style>
