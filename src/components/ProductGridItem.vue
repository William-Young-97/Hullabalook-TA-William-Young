<template>
  <div class="product-grid-item">
    <div v-for="product in products" :key="product.name" class="card">
      <img
        class="product-image"
        :src="product.image"
        :alt="`Image of ${product.name}`"
      />
      <div class="product-info">
        <p class="product-name">{{ product.name }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductGridItem',
  props: {
    products: { type: Array, required: true, default: () => [] },
  },
};
</script>

<style scoped>
.product-grid-item {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  padding: 100px;
}

.card {
  display: flex;
  flex-direction: column;
  text-align: center;
  border-width: 10px;
  width: 300px;
  max-width: 100%;
}

.product-image {
  width: 100%;
  align-self: center;
}

.product-info > * {
  overflow-wrap: break-word;
  width: 100%;
  text-align: center;
}

.product-name {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: -50px;
  z-index: 1;
  align-self: center;
  width: 80%;
  background-color: whitesmoke;
  padding: 5px;
}
</style>
