<template>
  <div class="product-grid-item">
    <div v-for="product in products" :key="product.name" class="card">
      <img
        class="product-image"
        :src="product.image"
        :alt="`Image of ${product.name}`"
      />
      <div class="product-info">
        <div class="info-background">
          <p class="product-name">{{ product.name }}</p>
          <p class="product-price">Price: £{{ product.price }}</p>
        </div>
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
  padding: 20px;
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

.product-info {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.info-background {
  background-color: whitesmoke; /* Add background color here */
  padding: 5px;
  width: 80%;
  text-align: center;
}

.product-name,
.product-price {
  margin: 5px;
}
</style>
