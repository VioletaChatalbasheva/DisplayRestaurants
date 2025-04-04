<template>
  <div class="selector">
    <label for="postcode">Select a UK postcode:</label>
    <select id="postcode" v-model="selected" @change="emitPostcode">
      <option disabled value="">-- Select a postcode --</option>
      <option v-for="pc in postcodes" :key="pc" :value="pc">{{ pc }}</option>
    </select>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selected: '',
      postcodes: [
        'CT1 2EH',
        'BS1 4DJ',
        'L4 0TH',
        'NE9 7TY',
        'SW1A 1AA',
        'CF11 8AZ',
        'M16 0RA',
        'EH1 1RE',
        'BN1 1AE',
        'CB7 4DL',
        'LS2 7HY',
        'G3 8AG',
        'PL4 0DW',
        'B26 3QJ',
        'DH4 5QZ',
        'BT7 1NN',
      ],
    }
  },
  methods: {
    emitPostcode() {
      this.$emit('postcode-selected', this.selected)
    },
  },
}
</script>

<style>
.selector {
  margin-bottom: 1rem;
}

select {
  padding: 0.5rem;
  margin-left: 1rem;
}
</style>
