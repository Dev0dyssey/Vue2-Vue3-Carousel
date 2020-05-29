<template>
  <v-app>
    <v-content class="text-center">
      <v-btn @click="showVue2">Vue 2 Option API</v-btn>
      <v-btn @click="showVue3">Vue 3 Composition API</v-btn>
      <span v-show="vue2">
        <CarouselContainerB />
      </span>
      <span v-show="vue3">
        <CarouselContainer />
      </span>
    </v-content>
  </v-app>
</template>

<script>
import CarouselContainer from "./components/CarouselContainer";
import CarouselContainerB from "./components/CarouselContainerB";

export default {
  name: "App",

  components: {
    CarouselContainer,
    CarouselContainerB
  },

  data: () => ({
    vue3: false,
    vue2: false
  }),
  methods: {
    showVue2() {
      this.vue2 = true;
      this.vue3 = false;
    },

    showVue3() {
      this.vue2 = false;
      this.vue3 = true;
    }
  }
};
</script>

<style lang="scss" scoped>
</style>