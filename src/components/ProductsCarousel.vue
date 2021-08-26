<template>
  <div class="shadow-lg">
    <a href="#">
      <img :src="product.image" class="rounded-tl-lg rounded-tr-lg" />
    </a>
    <div class="p-5">
      <h3 class="font-bold text-left">
        <a href="#">{{ product.title }}</a>
      </h3>
      <p class="font-bold text-sm text-left mb-2">
        ${{ product.price.toFixed(2) }}
      </p>
      <p class="text-left">
        <button class="uppercase bg-gray-900 text-gray-100 font-bold px-3 py-1" @click="addToCart()">
          Add to cart
        </button>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["product"],
  components: {},
  data() {
    return {};
  },
  methods: {
    addToCart() {
      this.$store.commit('addToCart', this.product)
    }
  }
};
</script>
