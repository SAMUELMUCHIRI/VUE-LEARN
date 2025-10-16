<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'
const products = ref('Socks')
const description = ref('A pair of warm, fuzzy socks')
const image = ref(socksBlueImage)
const url = ref('#')
const inventory = ref(100)
</script>

<template>
  <div class="nav-bar"></div>
    <div class="product-display">
        <div class="product-container">
          <div class="product-image"> 
            <a :href="url"><img :src="image"  ></a>
          </div>
          <div class="product-info">

            <h1>{{ products }}</h1>
            <p v-if="inventory > 10 ">In Stock</p>
            <p v-else-if="inventory <= 10 && inventory > 0">Almost Sold out </p>
            <p v-else>Out of Stock</p>
            <p>{{ description }}</p>
          </div>
        </div>
  </div>
</template>

<style scoped></style>
