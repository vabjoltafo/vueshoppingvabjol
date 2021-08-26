<template>
  <div class="container mx-auto lg:mt-20 text-gray-900 overflow-x-hidden">
    <div class="flex flex-row justify-between mb-4">
      <h2 class="text-xl font-bold ml-4 xl:mx-0">Best Sellers</h2>
    </div>
    <Carousel
      :settings="settings"
      :breakpoints="breakpoints"
      class="mx-4 xl:mx-0"
    >
      <Slide class="md:pr-8" v-for="product in products" :key="product.id">
        <ProductsCarousel :product="product" />
      </Slide>
      <template #addons>
        <Navigation
          class="invisible xl:visible mr-10 absolute -top-5 right-0"
        />
      </template>
    </Carousel>
    <h2 class="text-xl font-bold ml-4 xl:mx-0 lg:mt-20 mb-4">Shoes</h2>
    <div class="grid grid-flow-row grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8 mx-4 xl:mx-0">
      <ProductCard
      v-for="product in products"
      :key="product.id"
      :product="product"
    />
    </div>
    
  </div>
</template>

<script>
import products from "../data/products";
import ProductsCarousel from "./ProductsCarousel.vue";
import ProductCard from "./ProductCard.vue";
import { Carousel, Slide, Navigation } from "vue3-carousel";
import "vue3-carousel/dist/carousel.css";

export default {
  components: {
    ProductsCarousel,
    ProductCard,
    Carousel,
    Slide,
    Navigation,
  },
  data() {
    return {
      products: products,
      settings: {
        itemsToShow: 1,
        snapAlign: "center",
      },
      // breakpoints are mobile first
      // any settings not specified will fallback to the carousel settings
      breakpoints: {
        // 700px and up
        700: {
          itemsToShow: 2,
          snapAlign: "center",
        },
        // 1024 and up
        1024: {
          itemsToShow: 4,
          snapAlign: "start",
        },
        1366: {
          itemsToShow: 4,
          snapAlign: "start",
          mouseDrag: false,
        },
      },
    };
  },
};
</script>
