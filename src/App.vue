<template>
  <div class="app">
    <h1>Restaurant Finder</h1>
    <PostcodeSelector @postcode-selected="fetchRestaurants" />

    <div v-if="loading">Loading...</div>
    <div v-else-if="restaurants.length">
      <RestaurantList :restaurants="restaurants" />
    </div>
    <div v-else-if="selectedPostcode">
      <p>No restaurants found.</p>
    </div>
  </div>
</template>

<script>
import PostcodeSelector from './components/PostcodeSelector.vue'
import RestaurantList from './components/RestaurantList.vue'

export default {
  components: {
    PostcodeSelector,
    RestaurantList,
  },
  data() {
    return {
      restaurants: [],
      loading: false,
      selectedPostcode: null,
    }
  },
  methods: {
    async fetchRestaurants(postcode) {
      this.selectedPostcode = postcode
      this.restaurants = []
      this.loading = true

      try {
        const base = 'https://uk.api.just-eat.io/discovery/uk/restaurants/enriched/bypostcode/'
        const cleanPostcode = postcode.replace(/\s+/g, '')
        const targetUrl = base + cleanPostcode

        // Use ThingProxy to bypass CORS instead of a server-side proxy
        const proxyUrl = `https://thingproxy.freeboard.io/fetch/${targetUrl}`
        const response = await fetch(proxyUrl, {
          headers: { Accept: 'application/json' },
        })
        const data = await response.json()

        // console.log(data.restaurants)

        // Display only the first 10 restaurants
        this.restaurants = (data.restaurants || []).slice(0, 10).map((r) => ({
          name: r.name,
          cuisines: r.cuisines.map((c) => c.name).join(', '),
          rating: r.rating.starRating,
          address: `${r.address.firstLine}, ${r.address.city}`,
        }))
      } catch (error) {
        console.error('Failed to fetch data:', error)
      } finally {
        this.loading = false
      }
    },
  },
}
</script>

<style>
body {
  font-family: sans-serif;
  margin: 2rem;
  background: #f7f7f7;
}

.app {
  max-width: 700px;
  margin: auto;
}
</style>
