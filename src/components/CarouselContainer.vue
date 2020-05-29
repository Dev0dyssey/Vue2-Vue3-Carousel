<template>
  <v-container class="d-flex flex-column">
    <v-row class="d-flex">
      <v-col class="d-flex flex-column justify-space-between" cols="12">
        <v-row>
          <v-col cols="12" class="orderSection" v-show="order.length">
            <h2>Your orders</h2>
            <span v-for="(item, index) in order" :key="index">
              <h4>{{ item.item }} - £{{item.price}}</h4>
            </span>
            <h2 class="total">Total: £{{orderTotal}}</h2>
            <v-btn depressed color="success" @click="serverCall">Place order</v-btn>
          </v-col>
          <v-col cols="12" md="4">
            <v-img src="https://bit.ly/36H3kIm" height="100%"></v-img>
          </v-col>
          <v-col cols="12" md="8" class="d-flex text-justify flex-column justify-space-between">
            <p>
              Cliche vexillologist bushwick, cold-pressed lomo commodo proident actually freegan skateboard yr hoodie ut. Mlkshk photo booth adaptogen locavore lyft viral
              artisan, chartreuse poutine dreamcatcher blog roof party put a bird on it selfies. Vape messenger bag YOLO, kombucha disrupt dolore direct trade quinoa.
              Poke woke 3 wolf moon everyday carry do sustainable blue bottle copper mug cillum actually four loko chia pariatur keffiyeh vexillologist.
              Meggings chia etsy labore meditation actually. Pinterest poutine next level, voluptate laboris migas ennui intelligentsia activated charcoal nisi.
            </p>
            <h3>Price: £100</h3>
          </v-col>
        </v-row>
        <v-row>
          <v-col class="d-flex flex-column text-center justify-end">
            <h1>Customers also bought</h1>
            <v-sheet class="mx-auto" style="width: 100%;">
              <v-slide-group v-model="model" class="pa-4" show-arrows>
                <v-slide-item
                  v-for="(item, index) in carouselData"
                  :key="index"
                  v-slot:default="{ active, toggle }"
                >
                  <v-card class="ma-4" height="250" width="200" @click="toggle">
                    <v-list-item>
                      <v-list-item-content>
                        <v-list-item-title class="headline">{{ item.name }}</v-list-item-title>
                        <v-list-item-subtitle>£ {{ item.price.formattedValue }}</v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                    <v-img :src="item.productImageUrl" :alt="item.productImageAltText" contain></v-img>
                    <v-card-actions style="justify-content: center">
                      <v-btn
                        depressed
                        color="success"
                        @click="addToOrder(item.name, item.price.formattedValue)"
                      >Add</v-btn>
                    </v-card-actions>
                  </v-card>
                </v-slide-item>
              </v-slide-group>
              <v-expand-transition>
                <v-sheet v-if="model != null" color="grey lighten-4" height="200" tile>
                  <v-row class="fill-height" align="start" style="text-align: left">
                    <v-col cols="12" md="6">
                      <h3 class="title">{{ carouselData[model].name }}</h3>
                    </v-col>
                    <v-col cols="12" md="6">
                      <h4>Product Details:</h4>
                      <v-row>
                        <v-col cols="12">
                          <p>
                            Poke ugh plaid commodo truffaut vexillologist prism. Tumblr chicharrones austin consectetur vice kinfolk ut shoreditch palo santo gluten-free yuccie.
                            Vape wolf leggings minim four loko. Glossier chambray meh magna brooklyn sartorial voluptate etsy cliche paleo irure.
                          </p>
                        </v-col>
                      </v-row>
                    </v-col>
                  </v-row>
                  <v-row justify="start"></v-row>
                </v-sheet>
              </v-expand-transition>
            </v-sheet>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { ref, watchEffect } from "@vue/composition-api";
import json from "../json/data.json";

export default {
  name: "CarouselContainer",
  components: {},
  setup() {
    const { carouselData } = json;

    let model = ref(null);
    let order = ref([]);
    let orderTotal = ref(0);

    const addToOrder = (item, price) => {
      order.value.push({
        item,
        price
      });
      orderTotal.value += parseInt(price);
    };

    const serverCall = () => {
      console.log(`Send to server: ${order}`);
      order.value = [];
    };

    watchEffect(() => {
      console.log("This is the json: ", carouselData);
    });

    return {
      model,
      json,
      carouselData,
      order,
      orderTotal,
      addToOrder,
      serverCall
    };
  }
};
</script>

<style lang="scss" scoped>
.container {
  width: 100%;
  height: 100vh;
}

.orderSection {
  text-align: left;

  h4 {
    color: blue;
    text-decoration: underline;
  }
}
</style>