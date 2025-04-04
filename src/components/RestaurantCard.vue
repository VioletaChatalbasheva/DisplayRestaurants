<template>
  <div class="card">
    <h2>{{ restaurant.name }}</h2>
    <p><span style="font-weight: bold">Cuisines:</span> {{ restaurant.cuisines }}</p>
    <p>
      <span style="font-weight: bold">Rating:</span>
      {{ restaurant.rating }}
      <img
        src="@/assets/images/star_jet.jpg"
        alt="star"
        style="width: 30px; height: 30px; vertical-align: middle; margin-bottom: 5px"
      />
    </p>
    <p><span style="font-weight: bold">Address:</span> {{ restaurant.address }}</p>
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
  background: #fff;
  border: 1px solid #ff6600;
  border-radius: 8px;
  padding: 1rem;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
  margin-bottom: 1rem;
}

.card:hover {
  transform: scale(1.02);
}

.card h2 {
  color: #ff6600;
  margin-bottom: 0.5rem;
}

.card p {
  margin: 0.25rem 0;
  color: #333;
}
</style>
