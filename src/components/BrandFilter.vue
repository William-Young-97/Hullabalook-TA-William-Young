<template>
  <div>
    <div v-for="brand in brands" :key="brand">
      <input
        class="input"
        type="checkbox"
        :id="brand"
        :value="brand"
        v-model="selectedBrands"
      />
      <label :for="brand">{{ brand }}</label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BrandFilter',
  props: {
    products: {
      // Pass the full list of products as a prop
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      selectedBrands: [],
      brands: [],
    };
  },
  created() {
    this.brands = [...new Set(this.products.map((product) => product.brand))];
  },
  watch: {
    selectedBrands: function (newVal) {
      this.$emit('brandFilterApplied', newVal); // Emit the array of selected brands
    },
  },
};
</script>
