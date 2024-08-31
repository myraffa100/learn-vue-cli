<template>
  <div id="app" class="container mt-5">
    <h1>IDShop</h1>
    <!-- Penamaan yang sesuai -->
    <ProductList :products="products" :maximum="maximum"></ProductList>
  </div>
</template>

<script>
import ProductList from "./components/ProductList.vue";

export default {
  name: "App",
  data() {
    return {
      maximum: 50,
      products: [],
    };
  },
  components: {
    ProductList,
  },
  mounted() {
    fetch("https://hplussport.com/api/products/order/price")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
};
</script>
<!-- membersihkan format lint -->
<!-- npm run lint -- --fix -->