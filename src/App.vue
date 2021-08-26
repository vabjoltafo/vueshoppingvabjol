<template>
  <div class="bg-gray-100">
    <Home  />
    <Body />
  </div>
</template>

<script>
import Home from "./components/Home.vue";
import Body from './components/Body.vue';

export default {
  name: "App",
  components: {
    Home,
    Body
  },
};
</script>
