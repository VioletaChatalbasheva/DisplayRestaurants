<template>
  <div class="list">
    <RestaurantCard
      v-for="(restaurant, index) in restaurants"
      :key="index"
      :restaurant="restaurant"
    />
  </div>
</template>

<script>
import RestaurantCard from './RestaurantCard.vue'

export default {
  props: {
    restaurants: Array,
  },
  components: {
    RestaurantCard,
  },
}
</script>

<style>
.list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
</style>
