<template>
  <div v-if="product">
    <h1 class="text-2xl font-bold">{{ product.name }}</h1>
    <img :src="product.image" alt="Product Image" class="w-full h-64 object-cover" />
    <p class="mt-2">Price: ${{ product.price }}</p>
    <p class="mt-2">{{ product.description }}</p>
    <router-link to="/" class="text-blue-500 underline">Back to Product List</router-link>
  </div>
  <div v-else>
    <p>Loading...</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import { fetchProducts } from '@/services/ProductService';

const product = ref(null);
const route = useRoute();

const fetchProductData = async () => {
  const products = await fetchProducts();
  const productId = parseInt(route.params.id); // Отримуємо ID продукту з маршруту
  product.value = products.find(p => p.id === productId); 
};

onMounted(fetchProductData);
</script>
