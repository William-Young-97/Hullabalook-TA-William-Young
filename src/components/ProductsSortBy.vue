<template>
  <div>
    <select
      class="select"
      v-model="selectedSortOrder"
      @change="sortProductsBy(selectedSortOrder)"
    >
      <option value="default">Sort by Price or Relevance</option>
      <option value="descending">Price: High to Low</option>
      <option value="ascending">Price: Low to High</option>
      <option value="mostRelevant">Most Relevant</option>
      <option value="leastRelevant">Least Relevant</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'ProductSortBy',
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      selectedSortOrder: 'default',
    };
  },
  methods: {
    sortProductsByPrice(order) {
      if (order === 'ascending') {
        let ascending = [...this.products].sort((a, b) => a.price - b.price);
        this.$emit('sortedBy', ascending);
      } else if (order === 'descending') {
        let descending = [...this.products].sort((a, b) => b.price - a.price);
        this.$emit('sortedBy', descending);
      } else {
        let revert = [...this.products];
        this.$emit('sortedBy', revert);
      }
    },
    sortProductsByRelevance(order) {
      if (order === 'mostRelevant' || order === 'leastRelevant') {
        let sortedProducts = [...this.products].sort((a, b) => {
          if (a.isAvailable !== b.isAvailable) {
            return b.isAvailable - a.isAvailable;
          }

          return a.rank - b.rank;
        });

        if (order === 'leastRelevant') {
          sortedProducts.reverse();
        }

        this.$emit('sortedBy', sortedProducts);
      } else {
        let revert = [...this.products];
        this.$emit('sortedBy', revert);
      }
    },
    sortProductsBy(choice) {
      if (choice === 'ascending' || choice === 'descending') {
        this.sortProductsByPrice(choice);
      } else if (choice === 'mostRelevant' || choice === 'leastRelevant') {
        this.sortProductsByRelevance(choice);
      } else {
        this.$emit('sortedBy', [...this.products]);
      }
    },
  },
};
</script>
