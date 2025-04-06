<template>
  <div class="card">
    <h2>{{ restaurant.name }}</h2>
    <p><span style="font-weight: bold">Cuisines:</span> {{ restaurant.cuisines }}</p>
    <p><span style="font-weight: bold">Address:</span> {{ restaurant.address }}</p>
    <p>
      <span style="font-weight: bold">Rating:</span>
      {{ restaurant.rating }}
      <img
        v-if="restaurant.rating >= 3"
        src="@/assets/images/star_jet.jpg"
        alt="star"
        style="width: 20px; height: 20px; vertical-align: middle; margin-bottom: 4px"
      />
    </p>
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
  border: 1px solid #ff6600;
  border-radius: 8px;
  border-width: 2px;
  padding: 1rem;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  margin-bottom: 1rem;
}

.card:hover {
  transform: scale(1.02);
}

.card h2 {
  color: #ff6600;
  margin-top: 0;
}

.card p {
  margin: 0.5rem 0;
  color: #333;
  margin-bottom: 0;
}
</style>
