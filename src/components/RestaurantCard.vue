<!-- i want to display the fields of the restaurant with a placeholder -->
<template>
  <div class="restaurant-card">
    <p>Name of restaurant: {{ restaurant.name }}</p>
    <p>Address: {{ restaurant.address }}</p>
    <p>Rating: {{ restaurant.rating }}</p>
    <p>Cuisine: {{ restaurant.cuisine }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      restaurant: {
        name: 'Hangout',
        address: 'Delft',
        rating: 4.5,
        cuisine: 'asian',
      },
    }
  },
}
</script>
