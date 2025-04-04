<template>
  <div class="card">
    <h2>{{ restaurant.name }}</h2>
    <p><strong>Cuisines:</strong> {{ restaurant.cuisines }}</p>
    <p><strong>Rating:</strong> {{ restaurant.rating }}</p>
    <p><strong>Address:</strong> {{ restaurant.address }}</p>
  </div>
</template>

<script>
export default {
  props: {
    restaurant: Object,
  },
}
</script>

<style>
.card {
  background: white;
  border-radius: 8px;
  padding: 1rem;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}
</style>
