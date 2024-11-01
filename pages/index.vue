<template>
  <div>
    <MyHeader />
    <div class="mb-4">
      <label>Price Filter:</label>
      <select v-model="priceFilter">
        <option value="all">All</option>
        <option value="cheap">Cheap (under $30)</option>
        <option value="medium">Medium ($30-$70)</option>
        <option value="expensive">Expensive (over $70)</option>
      </select>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
      <ProductCard
        v-for="product in filteredProducts"
        :key="product.id"
        :product="product"
      />
    </div>
    <MyFooter />
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import { fetchProducts } from '@/services/ProductService'; 
import MyHeader from '@/components/MyHeader.vue'; 
import MyFooter from '@/components/MyFooter.vue'; 
import ProductCard from '@/components/ProductCard.vue'; 

const products = ref([]);
const priceFilter = ref('all');

const fetchProductData = async () => {
  products.value = await fetchProducts(); // Отримуємо дані через Axios
  console.log(products.value);  
};

const filteredProducts = computed(() => {
  if (priceFilter.value === 'cheap') {
    return products.value.filter(product => product.price < 30);
  } else if (priceFilter.value === 'medium') {
    return products.value.filter(product => product.price >= 30 && product.price <= 70);
  } else if (priceFilter.value === 'expensive') {
    return products.value.filter(product => product.price > 70);
  }
  return products.value; 
});

onMounted(fetchProductData); 
</script>

<style scoped>

</style>
