<script setup>
import { computed, defineProps, ref, toRefs } from "vue";
import ProductCardDetails from "./ProductCardDetails.vue";
import ProductCardImageHeader from "./ProductCardImageHeader.vue";
import ProductCardVariants from "./ProductCardVariants.vue";

const props = defineProps({
  productInfo: {
    required: true,
  },
});

const { productInfo } = toRefs(props);
const emit = defineEmits(["add-to-cart"]);

const selectedVariant = ref("Default");
const selectedSize = ref(null);

const updateVariant = (variant) => {
  selectedVariant.value = variant;
};

const updateSize = (size) => {
  selectedSize.value = size;
  console.log(selectedSize);
};

const currentStock = computed(() => {
  const inventoryItem = productInfo.value.productInventory.find(
    (item) => item.key === selectedVariant.value
  );
  return inventoryItem ? inventoryItem.stock : 0;
});

const currentPrice = computed(() => {
  const inventoryItem = productInfo.value.price.find(
    (item) => item.key === selectedVariant.value
  );

  return inventoryItem ? inventoryItem.amount : 0;
});

const discountedPrice = computed(() => {
  const price = (currentPrice.value * productInfo.value.salesAmount) / 100;
  return currentPrice.value - price;
});

const addToCart = () => {
  emit("add-to-cart");
  const inventoryItem = productInfo.value.productInventory.find(
    (item) => item.key === selectedVariant.value
  );
  inventoryItem.stock--;
};
</script>

<template>
  <div
    class="max-w-md w-full bg-white/10 backdrop-blur-lg rounded-2xl shadow-xl overflow-hidden border border-white/20"
  >
    <ProductCardImageHeader
      :productInfo="productInfo"
      :currentStock="currentStock"
      :selectedVariant="selectedVariant"
    />

    <div class="p-5">
      <ProductCardDetails
        :productInfo="productInfo"
        :currentStock="currentStock"
      />

      <ProductCardVariants
        :productInfo="productInfo"
        :selectedVariant="selectedVariant"
        @update-variant="updateVariant"
        @update-size="updateSize"
      />

      <!-- Product Details -->
      <div class="mb-4">
        <label class="block text-gray-200 text-xs font-semibold mb-2"
          >Product Details</label
        >
        <ul class="space-y-1">
          <li
            v-for="(detail, index) in productInfo.details"
            :key="index"
            class="text-gray-300 text-xs flex items-center gap-2"
          >
            <span class="w-1 h-1 bg-purple-400 rounded-full"></span>
            {{ detail }}
          </li>
        </ul>
      </div>

      <div class="text-gray-300 text-xs mb-4 flex gap-1">
        <div :class="[productInfo.onSale ? 'line-through' : '']">
          <span class="font-semibold">Price :</span>
          {{ currentPrice }} BDT
        </div>
        <span v-if="productInfo.onSale" class="text-yellow-300">
          Discounted Price {{ discountedPrice }} BDT</span
        >
      </div>

      <!-- Shop Now Button -->
      <div class="flex gap-2">
        <a
          :href="productInfo.productLink"
          class="flex-1 inline-flex items-center justify-center gap-2 px-4 py-2.5 bg-gradient-to-r from-blue-600 to-purple-600 text-white font-semibold rounded-xl shadow-lg hover:shadow-xl transition-all duration-300 transform hover:scale-105"
        >
          <span>Shop Now</span>
          <svg
            class="w-4 h-4"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M13 7l5 5m0 0l-5 5m5-5H6"
            ></path>
          </svg>
        </a>
        <button
          :class="[
            'flex-1 inline-flex items-center justify-center gap-2 px-4 py-2.5   font-semibold rounded-xl shadow-lg hover:shadow-xl transition-all duration-300 transform hover:scale-105',
            currentStock <= 0
              ? 'bg-red-700 text-white cursor-not-allowed'
              : 'bg-gradient-to-r from-gray-300 to-stone-200 text-black cursor-pointer',
          ]"
          v-on:click="addToCart"
          :disabled="currentStock <= 0"
        >
          <svg
            class="w-4 h-4"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M3 3h2l.4 2M7 13h10l4-8H5.4m0 0L7 13m0 0l-1.5 6M7 13l-1.5 6m1.5-6h10m0 0v6a2 2 0 01-2 2H9a2 2 0 01-2-2v-6m8 0V9a2 2 0 00-2-2H9a2 2 0 00-2 2v4.01"
            ></path>
          </svg>
          <span v-if="currentStock > 0"> Add to Cart</span>
          <span v-else>Out of Stock</span>
        </button>
      </div>
    </div>
  </div>
</template>
