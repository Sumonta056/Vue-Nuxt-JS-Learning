<script setup>
import { ref } from "vue";

const productInfo = ref({
  productName: "Shoes",
  productDescription: "Here, You get topic quality shoe",
  productLink: "www.google.com",
  productImage:
    "https://images.unsplash.com/photo-1608231387042-66d1773070a5?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&q=80&w=1074",
  productInventory: 160,
  onSale: true,
});
</script>

<template>
  <div
    class="min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900 flex justify-center items-center p-4"
  >
    <div
      class="max-w-4xl w-full bg-white/10 backdrop-blur-lg rounded-3xl shadow-2xl overflow-hidden border border-white/20"
    >
      <div class="lg:flex">
        <div class="lg:w-1/2 relative">
          <img
            class="h-64 w-full object-cover lg:h-full"
            :src="productInfo.productImage"
            :alt="productInfo.productName"
          />
          <div
            class="absolute inset-0 bg-gradient-to-t from-black/30 to-transparent"
          ></div>
        </div>

        <div class="lg:w-1/2 p-8 lg:p-12">
          <div class="flex items-center gap-3 mb-6">
            <h1 class="text-3xl lg:text-4xl font-bold text-white">
              {{ productInfo.productName }}
            </h1>
            <span
              v-if="productInfo.onSale"
              class="px-3 py-1 bg-gradient-to-r from-red-500 to-pink-500 text-white text-sm font-semibold rounded-full"
            >
              SALE
            </span>
            <span
              v-else
              class="px-3 py-1 bg-gradient-to-r from-green-500 to-emerald-500 text-white text-sm font-semibold rounded-full"
            >
              10% OFF
            </span>
          </div>

          <p class="text-gray-300 text-lg leading-relaxed mb-8">
            {{ productInfo.productDescription }}
          </p>

          <div class="mb-8">
            <div class="flex items-center gap-2 mb-2">
              <div
                class="w-3 h-3 rounded-full"
                :class="{
                  'bg-green-400': productInfo.productInventory >= 30,
                  'bg-yellow-400':
                    productInfo.productInventory >= 11 &&
                    productInfo.productInventory <= 29,
                  'bg-red-400': productInfo.productInventory < 11,
                }"
              ></div>
              <span class="text-white font-medium">
                <span v-if="productInfo.productInventory >= 30">In Stock</span>
                <span
                  v-else-if="
                    productInfo.productInventory >= 11 &&
                    productInfo.productInventory <= 29
                  "
                  >Limited Stock</span
                >
                <span v-else>Out of Stock</span>
              </span>
            </div>
            <p class="text-gray-400 text-sm">
              {{ productInfo.productInventory }} items available
            </p>
          </div>

          <a
            :href="productInfo.productLink"
            class="inline-flex items-center gap-2 px-8 py-4 bg-gradient-to-r from-blue-600 to-purple-600 text-white font-semibold rounded-2xl shadow-lg hover:shadow-xl transition-all duration-300 ease-in-out transform hover:scale-105 hover:from-blue-700 hover:to-purple-700"
          >
            <span>Shop Now</span>
            <svg
              class="w-5 h-5"
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
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
