<template>
  <div class="app">
    <div ref="header" class="header-column">
      <img class="logo" src="@/assets/images/just-eat-logo.png" alt="Just Eat Takeaway Logo" />
      <h1>Restaurant Finder</h1>
      <PostcodeSelector @postcode-selected="fetchRestaurants" />
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
  mounted() {
    // After the component mounts, measure the header height
    const headerHeight = this.$refs.header.offsetHeight
    console.log('Header height:', headerHeight)
    // Set a CSS variable on the root element
    document.documentElement.style.setProperty('--header-height', headerHeight + 'px')
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
  padding: 0;
}

.header-column {
  position: fixed;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #fff;
  padding: 1rem;
  z-index: 9999;
  width: 100%;
  box-sizing: border-box;
}

.logo {
  max-height: 60px;
  margin-bottom: 1rem;
}

.content {
  margin-top: var(--header-height);
  max-width: 700px;
  margin-left: auto;
  margin-right: auto;
}
</style>
