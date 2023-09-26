<template>
  <div class="app" ref="app-container">
    <h3>Filters</h3>
    <div class="filters">
      <div class="filter-row">
        <StockFilter
          class="stock-filter"
          :products="allProducts"
          @stockFilterApplied="updateStockFilter"
        />
        <div class="sort-drop-down">
          <ProductSortBy
            class="sort-by"
            :products="displayedProducts"
            @sortedBy="displayedProducts = $event"
          />
        </div>
        <div class="title">SHOE PRODUCT LISTING PAGE</div>
        <!-- Add this div for the title -->
      </div>
      <BrandFilter
        class="brand-filter"
        :products="allProducts"
        @brandFilterApplied="updateBrandFilter"
      />
    </div>

    <div class="display-count">
      <ProductCountDisplay :productCount="displayedProducts.length" />
    </div>

    <div class="product-grid">
      <ProductGridItem :products="displayedProducts" />
    </div>
  </div>
</template>

<script>
import ProductGridItem from './components/ProductGridItem.vue';
import StockFilter from './components/StockFilter.vue';
import BrandFilter from './components/BrandFilter.vue';
import ProductCountDisplay from './components/DisplayCounter.vue';
import ProductSortBy from './components/ProductsSortBy.vue';
import products from './data/products.json';

export default {
  name: 'App',
  components: {
    ProductGridItem,
    StockFilter,
    BrandFilter,
    ProductCountDisplay,
    ProductSortBy,
  },
  data() {
    return {
      allProducts: products,
      displayedProducts: products,
      stockFilterState: false,
      brandFilterState: [],
    };
  },
  methods: {
    updateBrandFilter(brands) {
      this.brandFilterState = brands;
      this.applyAllFilters();
    },
    updateStockFilter(isFilterActive) {
      this.stockFilterState = isFilterActive;
      this.applyAllFilters();
    },
    applyAllFilters() {
      let filteredProducts = this.allProducts;

      // Apply Stock Filter
      if (this.stockFilterState) {
        filteredProducts = filteredProducts.filter(
          (product) => product.isAvailable
        );
      }

      // Apply Brand Filter
      if (this.brandFilterState.length > 0) {
        filteredProducts = filteredProducts.filter((product) =>
          this.brandFilterState.includes(product.brand)
        );
      }

      this.displayedProducts = filteredProducts;
    },
  },
};
</script>

<style>
body,
html {
  margin: 0;
  padding: 0;
  height: auto;
  background: linear-gradient(to bottom, #add8e6, white);
}

.app {
  max-width: 1024px;
  margin: 0 auto;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  color: #606569;
  font-weight: bold;
}

.filter-row {
  display: flex;
  align-items: center;
  gap: 20px;
  justify-content: space-between;
}

.title {
  flex-grow: 2;
  text-align: right;
  font-size: 1.5rem;
}

.stock-filter,
.sort-drop-down {
  margin-bottom: 15px;
}

.display-count {
  margin-top: 15px;
}
</style>
