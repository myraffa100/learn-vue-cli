<template>
  <transition-group
    name="fade"
    tag="div"
    @beforeEnter="beforeEnter"
    @enter="enter"
    @leave="leave"
  >
    <div
      v-for="(item, index) in showItem"
      :key="item.id"
      class="row d-none mb-3 align-items-center"
      :data-index="index"
    >
      <div class="col-1 m-auto">
        <button class="btn btn-info" @click="$emit('add', item)">+</button>
      </div>
      <div class="col-sm-4">
        <img :src="item.image" :alt="item.name" class="img-fluid d-block" />
      </div>
      <div class="col">
        <h3 class="text-info">{{ item.name }}</h3>
        <p class="mb-0">{{ item.description }}</p>
        <div class="h5 float-right">
          <ProductPrice
            :value="Number(item.price)"
            :prefix="'Rp'"
            :precision="2"
          ></ProductPrice>
        </div>
      </div>
    </div>
  </transition-group>
</template>

<script>
import ProductPrice from "./ProductPrice.vue";

export default {
  name: "ProductList",
  components: {
    ProductPrice,
  },
  props: ["products", "maximum"],
  computed: {
    showItem() {
      let max = this.maximum;
      return this.products.filter(function (item) {
        return item.price <= max;
      });
    },
  },
  methods: {
    beforeEnter(el) {
      el.className = "d-none";
    },
    enter(el) {
      const delay = el.dataset.index * 100;
      setTimeout(() => {
        el.className =
          "row d-flex mb-3 align-items-center animate__animated animate__fadeInRight";
      }, delay);
    },
    leave(el) {
      const delay = el.dataset.index * 100;
      setTimeout(() => {
        el.className =
          "row d-flex mb-3 align-items-center animate__animated animate__fadeOutRight";
      }, delay);
    },
  },
};
</script>

<style scoped>
/* Tambahkan gaya kustom jika diperlukan */
</style>
