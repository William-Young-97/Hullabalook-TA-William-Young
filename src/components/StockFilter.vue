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
  data() {
    return {
      isFilterActive: false,
    };
  },
  methods: {
    toggleFilter() {
      this.isFilterActive = !this.isFilterActive;
      this.$emit('stockFilterApplied', this.isFilterActive);
    },
  },
};
</script>
