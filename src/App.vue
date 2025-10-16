<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'
const products = ref('Socks')
const description = ref('A pair of warm, fuzzy socks')
const image = ref(socksBlueImage)
const url = ref('#')
const inventory = ref(100)
const onSale = ref(true)
const details = ref(['50% cotton', '20% polyester', '30% wool'])
const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage, quantity: 0 },
  { id: 2235, color: 'blue', image: socksBlueImage, quantity: 10 },
])
const sizes = ref(['S', 'M', 'L', 'XL', 'XXL'])
const cart = ref(0)
const addToCart = () => {
  cart.value += 1
}

const updateImage = (variantImage) => {
  image.value = variantImage
}
</script>

<template>
  <div class="nav-bar"></div>
  <div class="cart p-4 text-right font-bold">Cart({{ cart }})</div>
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
            <p v-if="onSale" class="p-2 rounded-lg text-white bg-green-400 w-max">On Sale!</p>
            <p>{{ description }}</p>
            <ul class="flex flex-row gap-2">
              <li v-for="detail in details" :key="detail" class="p-2 rounded-lg bg-white/70 font-bold  text-sm border-0 border-green-700">{{ detail }}</li>             
            </ul>
             <div class="flex flex-row gap-4 my-2"><p>Sizes</p><p  v-for="variant in variants" :key="variant.id" :class="{'bg-green-400': variant.color === 'green',
              'bg-blue-400': variant.color === 'blue'
             }" class="border border-black px-2  rounded-lg" @mouseover="updateImage(variant.image)">{{variant.color}}</p></div>
             <div class="flex flex-row  w-max gap-4">
              <ul v-for="size in sizes" :key="size" class="p-4 font-sans rounded-lg bg-white/70 font-bold  text-sm border-0 border-green-700 ">
                {{size}}
              </ul>
                </div>
              <button @click="addToCart" class="button">Add to Cart</button>
          </div>
        </div>
  </div>
</template>

<style scoped></style>
