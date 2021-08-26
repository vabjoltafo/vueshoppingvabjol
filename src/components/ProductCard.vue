<template>
    <div class="shadow-lg">
        <a href="#">
          <img
            :src="product.image"
            class="rounded-tl-lg rounded-tr-lg"
          />
        </a>
        <div class="p-5">
          <h3 class="font-bold"><a href="#">{{ product.title }}</a></h3>
          <p class="font-bold text-sm mb-2">${{ product.price.toFixed(2)}}</p>
          <button @click="addToCart()" class="uppercase bg-gray-900 text-gray-100 font-bold px-3 py-1">
            Add to cart
          </button>
        </div>
      </div>
</template>

<script>
export default {
  props: ['product'],
  methods: {
    addToCart() {
      this.$store.commit('addToCart', this.product)
    }
  }
}
</script>