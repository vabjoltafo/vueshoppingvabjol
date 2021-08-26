<template>
  <header class="overflow-hidden">
    <nav
      class="container mx-auto mt-3 flex flex-col lg:flex-row lg:items-center justify-between"
    >
      <div class="lg:flex lg:flex-row">
        <h2
          class="lg:text-4xl text-2xl text-center font-bold text-gray-900 ml-3"
        >
          OrderSpark
        </h2>
      </div>

      <div class="flex flex-row justify-center mx-3">
        <div
          @click="isOpen = !isOpen"
          class="lg:invisible flex-1 justify-between"
        >
          <i v-if="!isOpen" class="fas fa-bars text-gray-900 text-2xl"></i>
          <i v-if="isOpen" class="fas fa-times text-gray-900 text-2xl"></i>
        </div>

        <div class="lg:mr-10">
          <i
            @click.prevent="cartModal()"
            class="fas fa-shopping-bag text-2xl text-gray-900"
          ></i>
          <span
            v-if="cartTotal"
            class="text-xs bg-red-600 ml-1 font-bold text-gray-100 border-2 border-red-600 px-1 rounded-full"
            >{{ cartTotal }}</span
          >
        </div>
        <div
          v-if="modal"
          class="bg-gray-900 bg-opacity-10 absolute top-0 right-0 h-screen w-full flex items-center justify-center z-50"
        >
          <div class=" bg-white p-4 rounded-md w-auto xl:w-2/9">
            <div v-if="cartTotal">
              <h2 class="text-md xl:text-xl font-bold">Your Cart</h2>
              <div v-for="prod in products" :key="prod.id">
                <div class="flex flex-row">
                  <img :src="prod.image" alt="" class="w-20 h-20" />
                  <div class="mt-4 ml-3 mr-2">
                    <h2 class="font-bold">{{ prod.title }}</h2>
                    <p>${{ prod.price }}</p>
                    <p>Quantity: {{ prod.quantity }}</p>
                  </div>
                  <button
                    @click="this.$store.commit('removeFromCart', prod)"
                    class="uppercase bg-red-600 rounded-sm px-3 h-6 mt-5 ml-auto"
                  >
                    <i class="fas fa-times text-white"></i>
                  </button>
                </div>
              </div>
            </div>
            <h2 v-else>Your cart is empty!</h2>
            <hr class="border border-gray-900">
            <p class="mt-2 font-bold">Total price: ${{ totalPrice.toFixed(2) }}</p>
            <div class="flex flex-row justify-between mt-2">
              <button
                @click="cartModal()"
                class=" bg-red-600 text-white font-bold px-3 py-1 rounded-md"
              >
                Close
              </button>
              <button
                class="uppercase text-white font-bold bg-green-500 rounded-md px-3 py-1"
                v-if="cartTotal"
              >
                Checkout
              </button>
            </div>
          </div>
        </div>
      </div>
    </nav>
    <ul
      :class="isOpen ? 'visible' : 'invisible -mb-20'"
      class="text-gray-900 text-lg lg:mb-0 text-center font-bold gap-8 flex flex-col lg:flex-row flex-1 lg:visible lg:justify-center lg:items-center"
    >
      <li><a href="#" class="">Shop All</a></li>
      <li><a href="#" class="">Sneakers</a></li>
      <li><a href="#" class="">Slides</a></li>
    </ul>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      isOpen: false,
      modal: false,
    };
  },
  
  methods: {
    cartModal() {
      if (this.modal == false) {
        this.modal = true;
      } else {
        this.modal = false;
      }
    },
  },
  mounted() {
    this.$store.commit('updateCartFromLocalStorage')
  },
  computed: {
    cartTotal() {
      return this.$store.getters.cartQuantity
    },
    products() {
      return this.$store.getters.cartItems
    },
    totalPrice() {
      return this.$store.getters.totalPrice
    }
  }
};
</script>
