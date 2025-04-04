<template>
  <div class="app">
    <!-- <h1>Restaurant Finder</h1> -->
    <PostcodeSelector />
    <RestaurantList />
    <RestaurantCard />
  </div>
</template>

<script>
import PostcodeSelector from './components/PostcodeSelector.vue'
import RestaurantList from './components/RestaurantList.vue'
import RestaurantCard from './components/RestaurantCard.vue'

export default {
  name: 'App',
  components: {
    PostcodeSelector,
    RestaurantList,
    RestaurantCard,
  },
}
</script>
