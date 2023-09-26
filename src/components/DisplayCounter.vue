<template>
  <div class="product-count-display">
    Products on this page: {{ productCount }}
  </div>
</template>

<script>
export default {
  name: 'ProductCountDisplay',
  props: {
    productCount: {
      type: Number,
      required: true,
    },
  },
};
</script>
