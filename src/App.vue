<template>
  <div class="app">
    <div class="header-column">
      <img class="logo" src="@/assets/images/just-eat-logo.png" alt="Just Eat Takeaway Logo" />
      <h1>Search for Restaurants:</h1>
      <PostcodeSelector class="postcode-selector" @postcode-selected="fetchRestaurants" />
    </div>

    <div class="content">
      <div v-if="loading">Loading...</div>
      <div v-else-if="restaurants.length">
        <RestaurantList :restaurants="restaurants" />
      </div>
      <div v-else-if="selectedPostcode">
        <p>No restaurants found.</p>
      </div>
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
  margin: 0;
  padding: 2rem 0 0 0;
}

.app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.header-column {
  text-align: center;
}

.logo {
  max-height: 60px;
  margin-bottom: 1rem;
}

.postcode-selector {
  align-items: center;
}

.postcode-selector select {
  border: 1px solid #ff6600;
  border-radius: 4px;
  cursor: pointer;
}

.postcode-selector select:focus,
.postcode-selector select:active {
  outline: none;
  border-color: #ff6600;
}
</style>
