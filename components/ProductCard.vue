<template>
  <div class="border p-4 rounded shadow">
    <router-link :to="`/product/${product.id}`">
      <img :src="product.image" alt="Product Image" class="w-full h-32 object-cover mb-2" />
      <h3 class="font-bold">{{ product.name }}</h3>
      <p>\${{ product.price }}</p>
      <p>{{ product.description }}</p>
    </router-link>
  </div>
</template>

<script setup>
defineProps({
  product: {
    type: Object,
    required: true
  }
});
</script>
