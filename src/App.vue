<script setup>
import { computed, ref } from "vue";
import socksGreenImage from "./assets/images/socks_green.jpeg";
import socksBlueImage from "./assets/images/socks_blue.jpeg";
const products = ref("Socks");
const description = ref("A pair of warm, fuzzy socks");
const selectedVariant = ref(0);
const url = ref("#");
const inventory = ref(100);

const details = ref(["50% cotton", "20% polyester", "30% wool"]);
const brand = ref("Vue Mastery");

const variants = ref([
    { id: 2234, color: "green", image: socksGreenImage, quantity: 0 },
    {
        id: 2235,
        color: "blue",
        image: socksBlueImage,
        quantity: 10,
    },
]);

const sizes = ref(["S", "M", "L", "XL", "XXL"]);
const cart = ref(0);

const addToCart = () => {
    if (inStock.value) {
        cart.value += 1;
    }
};

const image = computed(() => {
    return variants.value[selectedVariant.value].image;
});
const removefromCart = () => {
    if (cart.value > 0) {
        cart.value -= 1;
    }
};

const updateVariant = (index) => {
    selectedVariant.value = index;
};

const title = computed(() => {
    return brand.value + " " + products.value;
});

const inStock = computed(() => {
    return variants.value[selectedVariant.value].quantity > 0;
});
</script>

<template>
    <div class="nav-bar"></div>

    <div class="cart p-4 text-right font-bold">Cart({{ cart }})</div>
    <div class="product-display">
        <div class="product-container">
            <div class="product-image">
                <a :href="url"
                    ><img
                        :src="image"
                        :class="{ 'out-of-stock-img': !inStock }"
                /></a>
            </div>
            <div class="product-info">
                <h1>{{ title }}</h1>
                <p v-if="inStock">In Stock</p>
                <p v-else>Out of Stock</p>

                <p>{{ description }}</p>
                <ul class="flex flex-row gap-2">
                    <li
                        v-for="detail in details"
                        :key="detail"
                        class="p-2 rounded-lg bg-white/70 font-bold text-sm border-0 border-green-700"
                    >
                        {{ detail }}
                    </li>
                </ul>
                <div class="flex flex-row gap-4 my-2">
                    <p>Sizes</p>
                    <p
                        v-for="(variant, index) in variants"
                        :key="variant.id"
                        :class="{
                            'bg-green-400': variant.color === 'green',
                            'bg-blue-400': variant.color === 'blue',
                        }"
                        class="border border-black px-2 rounded-lg"
                        @mouseover="updateVariant(index)"
                    >
                        {{ variant.color }}
                    </p>
                </div>
                <div class="flex flex-row w-max gap-4">
                    <ul
                        v-for="size in sizes"
                        :key="size"
                        class="p-4 font-sans rounded-lg bg-white/70 font-bold text-sm border-0 border-green-700"
                    >
                        {{
                            size
                        }}
                    </ul>
                </div>
                <div class="flex flex-row gap-4 my-4">
                    <button
                        @click="addToCart"
                        :disabled="!inStock"
                        :class="{ disabledButton: !inStock }"
                        class="bg-green-400 text-white rounded-lg p-2 font-bold"
                    >
                        + Add to Cart
                    </button>
                    <button
                        @click="removefromCart"
                        :disabled="!inStock"
                        :class="{ disabledButton: !inStock }"
                        class="bg-black text-white rounded-lg p-2 font-bold"
                    >
                        - Remove from Cart
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped></style>
