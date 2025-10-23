<script setup>
import { ref, watch } from "vue";

const productInfo = ref({
  productName: "Shoes",
  productDescription: "Here, You get topic quality shoe",
  productLink: "www.google.com",
  productImage: [
    {
      key: "Default",
      url: "https://images.unsplash.com/photo-1608231387042-66d1773070a5?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&q=80&w=1074",
    },
    {
      key: "Green",
      url: "https://images.unsplash.com/photo-1512990414788-d97cb4a25db3?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8Z3JlZW4lMjBzaG9lc3xlbnwwfHwwfHx8MA%3D%3D&fm=jpg&q=60&w=3000",
    },
    {
      key: "Blue",
      url: "https://arthurknight.com/media/catalog/product/cache/8723b12f6326e9bdc6bc191d0c49a6b8/e/l/electric-blue-suede-mens-driving-shoes-1.jpg",
    },
  ],
  productInventory: 160,
  onSale: true,
  sizes: ["L", "XL", "XXL"],
  details: ["Premium leather construction", "Cushioned memory foam insole", "Non-slip rubber outsole"],
  variant: ["Default", "Green", "Blue"],
});

const selectedSize = ref(null);
const selectedVariant = ref("Default");
const currentImage = ref(productInfo.value.productImage[0].url);

watch(selectedVariant, (newVariant) => {
  const object = productInfo.value.productImage.find(
    (img) => img.key == newVariant
  );
  currentImage.value = object?.url || productInfo.value.productImage[0].url;
});
</script>

<template>
  <div
    class="min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900 flex justify-center items-center p-4"
  >
    <div
      class="max-w-sm w-full bg-white/10 backdrop-blur-lg rounded-2xl shadow-xl overflow-hidden border border-white/20"
    >
      <!-- Image Section -->
      <div class="relative h-56">
        <img
          class="h-full w-full object-cover"
          :src="currentImage"
          :alt="productInfo.productName"
        />
        <div class="absolute top-3 right-3">
          <span
            v-if="productInfo.onSale"
            class="px-2 py-1 bg-red-500 text-white text-xs font-bold rounded-full"
          >
            SALE
          </span>
          <span
            v-else
            class="px-2 py-1 bg-green-500 text-white text-xs font-bold rounded-full"
          >
            10% OFF
          </span>
        </div>
      </div>

      <!-- Content Section -->
      <div class="p-5">
        <!-- Title & Stock -->
        <div class="flex items-start justify-between mb-2">
          <h2 class="text-xl font-bold text-white">
            {{ productInfo.productName }}
          </h2>
          <div class="flex items-center gap-1">
            <div
              class="w-2 h-2 rounded-full"
              :class="{
                'bg-green-400': productInfo.productInventory >= 30,
                'bg-yellow-400':
                  productInfo.productInventory >= 11 &&
                  productInfo.productInventory <= 29,
                'bg-red-400': productInfo.productInventory < 11,
              }"
            ></div>
            <span class="text-gray-300 text-xs">
              {{ productInfo.productInventory }} in stock
            </span>
          </div>
        </div>

        <!-- Description -->
        <p class="text-gray-300 text-sm mb-4">
          {{ productInfo.productDescription }}
        </p>

        <!-- Color Variants & Sizes Side by Side -->
        <div class="flex gap-4 mb-4">
          <!-- Color Variants -->
          <div class="flex-1">
            <label class="block text-gray-200 text-xs font-semibold mb-2"
              >Colors</label
            >
            <div class="flex gap-2">
              <button
                v-for="variant in productInfo.variant"
                :key="variant"
                @click="selectedVariant = variant"
                :class="[
                  'w-8 h-8 rounded-full transition-all duration-200',
                  selectedVariant === variant
                    ? 'ring-2 ring-white scale-110'
                    : 'hover:scale-105',
                  variant === 'Default' ? 'bg-gray-700' : '',
                  variant === 'Green' ? 'bg-green-600' : '',
                  variant === 'Blue' ? 'bg-blue-500' : '',
                ]"
                :title="variant"
              ></button>
            </div>
          </div>

          <!-- Sizes -->
          <div class="flex-1">
            <label class="block text-gray-200 text-xs font-semibold mb-2"
              >Sizes</label
            >
            <div class="flex gap-2">
              <button
                v-for="size in productInfo.sizes"
                :key="size"
                @click="selectedSize = size"
                :class="[
                  'px-3 py-1 text-sm font-semibold rounded-lg transition-all duration-200',
                  selectedSize === size
                    ? 'bg-purple-600 text-white'
                    : 'bg-white/10 text-gray-300 hover:bg-white/20',
                ]"
              >
                {{ size }}
              </button>
            </div>
          </div>
        </div>

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
            class="flex-1 inline-flex items-center justify-center gap-2 px-4 py-2.5 bg-gradient-to-r from-gray-300 to-stone-200 text-black font-semibold rounded-xl shadow-lg hover:shadow-xl transition-all duration-300 transform hover:scale-105"
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
            <span>Add to Cart</span>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
