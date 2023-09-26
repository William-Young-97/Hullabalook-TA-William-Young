<template>
  <div>
    <button class="button" @click="toggleFilter">
      {{ isFilterActive ? 'Show All Products' : 'Filter Products In Stock' }}
    </button>
  </div>
</template>

<script>
export default {
  name: 'StockFilter',
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      isFilterActive: false,
    };
  },
  methods: {
    toggleFilter() {
      this.isFilterActive = !this.isFilterActive;
      this.$emit('stockFilterApplied', this.isFilterActive); // Emit only the state
    },
  },
};
</script>
